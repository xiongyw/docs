# Background

- Created: 2025.6.2
- Last Updated: 2026.6.4

The purpose is to test iGPU throughput to Windows 11 VM, on `HP EliteDesk 800 G4 DM`, using PVE 8.4-1 which comes with qemu 9.2.0.

At high level, the process can be roughly divided into two steps:

1. Host config for preparing passthrough, mainly on enabling iommu, loading proper kernel drivers and blacklisting gpu drivers.
2. VM config, in terms of vbios, vm's bios/machine selection and configs

What can be achieved for Windows 11 VM:

- Graphic: passthrough the `UHD Graphics 630` as a PCIe device.
- Sound (via Bluebooth): passthrough the Bluetooth USB device, via id-based redirection.
- Mouse/Keyboard: passthrough a 2.4G USB-dangle receiver, also via id-based redirection.
- WiFi: passthrough WiFi as another PCIe device. This is optional as the VM can use bridged NIC.

Key observations:

- For iGPU passthrough, the VBIOS (ROM image) is vital. Dumping/extracting the VBIOS from firmware is complicated. We downloaded one for UHD630 from [the web](https://www.123pan.com/s/20P0Vv-d2A6H.html), which works only in [`legacy-igd` mode](https://github.com/qemu/qemu/blob/master/docs/igd-assign.txt#L48), making it the primary and exclusive graphics device in the VM. Requires `pc-i440fx` machine type and emulated VGA set to `none`.
- IOMMU group limitation: Linux kernel only passthrough **all** endpoints in an iommu group. Thus if a pcie endpoint (say A) belongs to an IOMMU group which also contains other endpoints (say B and C), it's not possible (or difficult) to only passthrough A while leaving B and C in the host. In this setup, as the audio device (`00:1f.3`) belongs to an IOMMU group contains other critical components for the host, it's not possible to passthrough it to Windows 11. The workaround is to passthrough the Bluetooth as an usb device to the VM and using a bluetooth speaker for sound.
- It seems that adding kernel cmdline option `pcie_acs_override=downstream,multifunction,id:8086:a348,id:8086:a370` does not change the IOMMU grouping in this machine, suggesting that [Q370 PCH (Platform Controller Hub)](https://www.intel.com/content/www/us/en/products/sku/133282/intel-q370-chipset/specifications.html) may not support ACS properly.
- It seems that manual `vfio_pci` binding may bypass kernel restriction in passthrough the whole group (at the security risk of DMA attack), but tests shown that passthroughing `0:1f.3` along causes host network `eno1` (`0:1f.5` in the same IOMMU group) been reset and disabled.
- There is only one USB controller `0:14.0`, and it also IOMMU-grouped with `0:14.2`. Passing through the usb controller to the VM will leave the host without USB capabilities. The proper way is to use id-based redirection for USB devices, such as mouse/keyboard (`062a:4101`) and Bluetooth (`8087:0aaa`).

# System Info

System info about the `HP EliteDesk 800 G4 DM`:

```
# inxi -xFm
System:
  Host: pve Kernel: 6.8.12-11-pve arch: x86_64 bits: 64 compiler: gcc v: 12.2.0 Console: pty pts/1
    Distro: Debian GNU/Linux 12 (bookworm)
Machine:
  Type: Desktop System: HP product: HP EliteDesk 800 G4 DM 35W v: SBKPF serial: 8CC92437VY
  Mobo: HP model: 83E2 v: KBC Version 07.D4.00 serial: PGVXV0F8JCBJ4M UEFI: HP
    v: Q21 Ver. 02.30.00 date: 12/31/2024
Memory:
  RAM: total: 15.4 GiB used: 1.58 GiB (10.3%)
  Array-1: capacity: 32 GiB slots: 2 EC: None max-module-size: 16 GiB note: est.
  Device-1: DIMM3 type: DDR4 size: 8 GiB speed: 2667 MT/s
  Device-2: DIMM1 type: DDR4 size: 8 GiB speed: 2667 MT/s
CPU:
  Info: 6-core model: Intel Core i5-8400T bits: 64 type: MCP arch: Coffee Lake rev: A cache:
    L1: 384 KiB L2: 1.5 MiB L3: 9 MiB
  Speed (MHz): avg: 1212 high: 3273 min/max: 800/3300 cores: 1: 800 2: 800 3: 3273 4: 800 5: 800
    6: 800 bogomips: 20399
  Flags: avx avx2 ht lm nx pae sse sse2 sse3 sse4_1 sse4_2 ssse3 vmx
Graphics:
  Device-1: Intel CoffeeLake-S GT2 [UHD Graphics 630] vendor: Hewlett-Packard driver: vfio-pci
    v: N/A arch: Gen-9.5 bus-ID: 00:02.0
  Display: server: No display server data found. Headless machine? tty: 115x43
  API: OpenGL Message: GL data unavailable in console for root.
Audio:
  Device-1: Intel Cannon Lake PCH cAVS vendor: Hewlett-Packard driver: vfio-pci bus-ID: 00:1f.3
Network:
  Device-1: Intel Cannon Lake PCH CNVi WiFi driver: vfio-pci v: N/A bus-ID: 00:14.3
  Device-2: Intel Ethernet I219-LM vendor: Hewlett-Packard driver: e1000e v: kernel port: N/A bus-ID: 00:1f.6
  ...
Bluetooth:
  Device-1: Intel Bluetooth 9460/9560 Jefferson Peak (JfP) type: USB driver: usbfs bus-ID: 1-14:3
  Report: This feature requires one of these tools: hciconfig/bt-adapter
...

# lspci -tvnn
-[0000:00]-+-00.0  Intel Corporation 8th Gen Core Processor Host Bridge/DRAM Registers [8086:3ec2]
           +-02.0  Intel Corporation CoffeeLake-S GT2 [UHD Graphics 630] [8086:3e92]
           +-12.0  Intel Corporation Cannon Lake PCH Thermal Controller [8086:a379]
           +-14.0  Intel Corporation Cannon Lake PCH USB 3.1 xHCI Host Controller [8086:a36d]
           +-14.2  Intel Corporation Cannon Lake PCH Shared SRAM [8086:a36f]
           +-14.3  Intel Corporation Cannon Lake PCH CNVi WiFi [8086:a370]
           +-16.0  Intel Corporation Cannon Lake PCH HECI Controller [8086:a360]
           +-16.3  Intel Corporation Cannon Lake PCH Active Management Technology - SOL [8086:a363]
           +-17.0  Intel Corporation SATA Controller [RAID mode] [8086:2822]
           +-1f.0  Intel Corporation Q370 Chipset LPC/eSPI Controller [8086:a306]
           +-1f.3  Intel Corporation Cannon Lake PCH cAVS [8086:a348]
           +-1f.4  Intel Corporation Cannon Lake PCH SMBus Controller [8086:a323]
           +-1f.5  Intel Corporation Cannon Lake PCH SPI Controller [8086:a324]
           \-1f.6  Intel Corporation Ethernet Connection (7) I219-LM [8086:15bb]

# lsusb -tv
/:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=xhci_hcd/10p, 10000M
    ID 1d6b:0003 Linux Foundation 3.0 root hub
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=xhci_hcd/16p, 480M
    ID 1d6b:0002 Linux Foundation 2.0 root hub
    |__ Port 1: Dev 2, If 1, Class=Human Interface Device, Driver=usbhid, 12M
        ID 062a:4101 MosArt Semiconductor Corp. Wireless Keyboard/Mouse
    |__ Port 1: Dev 2, If 0, Class=Human Interface Device, Driver=usbhid, 12M
        ID 062a:4101 MosArt Semiconductor Corp. Wireless Keyboard/Mouse
    |__ Port 14: Dev 3, If 0, Class=Wireless, Driver=btusb, 12M
        ID 8087:0aaa Intel Corp. Bluetooth 9460/9560 Jefferson Peak (JfP)
    |__ Port 14: Dev 3, If 1, Class=Wireless, Driver=btusb, 12M
        ID 8087:0aaa Intel Corp. Bluetooth 9460/9560 Jefferson Peak (JfP)
```

The following is the IOMMU group info after enabling IOMMU:

```
# find /sys/kernel/iommu_groups/ -type l|sort
/sys/kernel/iommu_groups/0/devices/0000:00:02.0
/sys/kernel/iommu_groups/1/devices/0000:00:00.0
/sys/kernel/iommu_groups/2/devices/0000:00:12.0
/sys/kernel/iommu_groups/3/devices/0000:00:14.0
/sys/kernel/iommu_groups/3/devices/0000:00:14.2
/sys/kernel/iommu_groups/4/devices/0000:00:14.3
/sys/kernel/iommu_groups/5/devices/0000:00:16.0
/sys/kernel/iommu_groups/5/devices/0000:00:16.3
/sys/kernel/iommu_groups/6/devices/0000:00:17.0
/sys/kernel/iommu_groups/7/devices/0000:00:1f.0
/sys/kernel/iommu_groups/7/devices/0000:00:1f.3
/sys/kernel/iommu_groups/7/devices/0000:00:1f.4
/sys/kernel/iommu_groups/7/devices/0000:00:1f.5
/sys/kernel/iommu_groups/7/devices/0000:00:1f.6
```

# Host Install

- ssh login as `root`
    - `useradd -s /usr/bin/bash bruin; usermod -a -G sudo bruin; mkdir /home/bruin; chown -R bruin:bruin /home/bruin; passwd bruin`
    - disable `root` login:
        - `/etc/ssh/sshd_config`: `PermitRootLogin no`
        - `sudo systemctl restart sshd`
    - logout
- login as `bruin` and `su root`

- apt source:
    - replace `/etc/apt/sources.list` with content from `https://mirrors.tuna.tsinghua.edu.cn/help/debian/`
    - change `/etc/apt/sources.list.d/pve-enterprise.list` by replace its content with `deb https://mirrors.tuna.tsinghua.edu.cn/proxmox/debian buster pve-no-subscription`
    - comment out content in `/etc/apt/sources.list.d/ceph.list`
- `apt update/upgrade`;
- `apt install sudo binutils build-essential git tig htop tmux inxi nmon parted ranger ncdu inxi ripgrep libguestfs-tools`
- install linux headers: `apt install pve-headers-$(uname -r)`. headers will be installed under `/usr/src/linux-headers-$(uname -r)` folder. a symlink to it will be created at `/lib/modules/$(uname -r)/build`.
- remove subscription popup: `sed -i.bak "s/data.status !== 'Active'/false/g" /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js && systemctl restart pveproxy.service`
- [install `netbird`](https://docs.netbird.io/how-to/installation), by `curl -fsSL https://pkgs.netbird.io/install.sh | sh`.

- At this point, the ip addr are `192.168.10.104/24` (for `eno1` via DHCP) and `100.102.89.174/16` (static address for `wt0` created by [netbird](https://netbird.io/)), and we have:

```
root@pve:~# uname -a
Linux pve 6.8.12-11-pve #1 SMP PREEMPT_DYNAMIC PMX 6.8.12-11 (2025-05-22T09:39Z) x86_64 GNU/Linux
root@pve:~# cat /proc/cmdline
BOOT_IMAGE=/boot/vmlinuz-6.8.12-11-pve root=/dev/mapper/pve-root ro quiet
root@pve:~# cat /proc/fb
0 i915drmfb
root@pve:~# cat /etc/network/interfaces
auto lo
iface lo inet loopback
iface eno1 inet manual
auto vmbr0
iface vmbr0 inet static
        address 192.168.10.104/24
        gateway 192.168.10.1
        bridge-ports eno1
        bridge-stp off
        bridge-fd 0
iface wlp0s20f3 inet manual
source /etc/network/interfaces.d/*
```

# Host Config for Passthrough

- Assuming `vt-d` is already enabled in BIOS.

    ```
    @pve:/home/bruin# dmesg|grep -i vt-d
    [    4.942296] i915 0000:00:02.0: [drm] VT-d active for gfx access
    ```

- Enable iommu via `grub cmdline`:

    - Edit `/etc/default/grub`: `GRUB_CMDLINE_LINUX_DEFAULT` to enable iommu and passthrough:

      ```
      GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on iommu=pt"
      ```

    - Run `update-grub`: use `grep iommo /boot/grub/grub.cfg` to confirm the updates.
- Enforce kernel modules binding:
    - Edit `/etc/modules`, add the following for loading these modules by default:

        ```
        vfio
        vfio_iommu_type1
        vfio_pci
        vfio_virqfd
        ```

    - Add `/etc/modprobe.d/vfio.conf`, with the following content:

        ```
        # don't load driver for iGPU and sound card
        blacklist i915
        blacklist snd_hda_intel
        blacklist snd_sof_pci_intel_cnl

        # load vfio-pci driver instead
        options vfio-pci ids=8086:3e92,8086:a348

        #
        options kvm ignore_msrs=1
        options vfio_iommu_type1 allow_unsafe_interrupts=1
        ```

    - Run `update-initramfs -u -k all` to update initramfs accordingly for all kernels.

- Reboot the host, check that IOMMU is enabled and PVE host is not using the iGPU (the display should frees around `Loading initial ramdisk ...`).

    ```
    # dmesg |grep -e EMAR -e IOMMU -e AMD-Vi
    [    0.000000] Warning: PCIe ACS overrides enabled; This may allow non-IOMMU protected peer-to-peer DMA
    [    0.050582] DMAR: IOMMU enabled
    [    0.147791] DMAR-IR: IOAPIC id 2 under DRHD base  0xfed91000 IOMMU 1
    [    0.500116] DMAR: IOMMU feature fl1gp_support inconsistent
    [    0.500118] DMAR: IOMMU feature pgsel_inv inconsistent
    [    0.500120] DMAR: IOMMU feature nwfs inconsistent
    [    0.500122] DMAR: IOMMU feature pasid inconsistent
    [    0.500124] DMAR: IOMMU feature eafs inconsistent
    [    0.500125] DMAR: IOMMU feature prs inconsistent
    [    0.500127] DMAR: IOMMU feature nest inconsistent
    [    0.500129] DMAR: IOMMU feature mts inconsistent
    [    0.500130] DMAR: IOMMU feature sc_support inconsistent
    [    0.500132] DMAR: IOMMU feature dev_iotlb_support inconsistent

    root@pve:~# dmesg|grep 00:02.0
    [    0.390062] pci 0000:00:02.0: [8086:3e92] type 00 class 0x030000 PCIe Root Complex Integrated Endpoint
    [    0.390092] pci 0000:00:02.0: BAR 0 [mem 0xe0000000-0xe0ffffff 64bit]
    [    0.390098] pci 0000:00:02.0: BAR 2 [mem 0xd0000000-0xdfffffff 64bit pref]
    [    0.390102] pci 0000:00:02.0: BAR 4 [io  0x3000-0x303f]
    [    0.390126] pci 0000:00:02.0: Video device with shadowed ROM at [mem 0x000c0000-0x000dffff]
    [    0.432419] pci 0000:00:02.0: vgaarb: setting as boot VGA device
    [    0.432419] pci 0000:00:02.0: vgaarb: bridge control possible
    [    0.432419] pci 0000:00:02.0: vgaarb: VGA device added: decodes=io+mem,owns=io+mem,locks=none
    [    0.486672] pci 0000:00:02.0: Adding to iommu group 0
    [    2.949009] vfio-pci 0000:00:02.0: vgaarb: deactivate vga console
    [    2.949013] vfio-pci 0000:00:02.0: vgaarb: VGA decodes changed: olddecodes=io+mem,decodes=io+mem:owns=io+mem

    root@pve:~# dmesg|grep 00:1f.3
    [    0.396804] pci 0000:00:1f.3: [8086:a348] type 00 class 0x040300 conventional PCI endpoint
    [    0.396931] pci 0000:00:1f.3: BAR 0 [mem 0x4000100000-0x4000103fff 64bit]
    [    0.396947] pci 0000:00:1f.3: BAR 4 [mem 0x4000000000-0x40000fffff 64bit]
    [    0.397078] pci 0000:00:1f.3: PME# supported from D3hot D3cold
    [    0.486934] pci 0000:00:1f.3: Adding to iommu group 7

    # find /sys/kernel/iommu_groups/ -type l|sort
    /sys/kernel/iommu_groups/0/devices/0000:00:02.0
    /sys/kernel/iommu_groups/1/devices/0000:00:00.0
    /sys/kernel/iommu_groups/2/devices/0000:00:12.0
    /sys/kernel/iommu_groups/3/devices/0000:00:14.0
    /sys/kernel/iommu_groups/3/devices/0000:00:14.2
    /sys/kernel/iommu_groups/4/devices/0000:00:14.3
    /sys/kernel/iommu_groups/5/devices/0000:00:16.0
    /sys/kernel/iommu_groups/5/devices/0000:00:16.3
    /sys/kernel/iommu_groups/6/devices/0000:00:17.0
    /sys/kernel/iommu_groups/7/devices/0000:00:1f.0
    /sys/kernel/iommu_groups/7/devices/0000:00:1f.3
    /sys/kernel/iommu_groups/7/devices/0000:00:1f.4
    /sys/kernel/iommu_groups/7/devices/0000:00:1f.5
    /sys/kernel/iommu_groups/7/devices/0000:00:1f.6

    # lspci -s 0:2.0 -vv|grep -i "kernel"
            Kernel driver in use: vfio-pci
            Kernel modules: i915

    # lspci -s 0:1f.3 -vv|grep -i "kernel"
            Kernel driver in use: vfio-pci
            Kernel modules: snd_hda_intel, snd_sof_pci_intel_cnl

    # lsmod|grep i915
    # lsmod|grep snd
    # cat /proc/fb
    ```

# Clone a Win11 VM from Another PVE Host

```
root@pve:~# qemu-system-x86_64 --version
QEMU emulator version 9.2.0 (pve-qemu-kvm_9.2.0-5)
Copyright (c) 2003-2024 Fabrice Bellard and the QEMU Project developers
```

A win11 debloated installation has been done on another pve host (with vm id `103`). The purpose is to clone it to the new pve host (with vm id `100`).

The original vm config:

```
# qm config 103
agent: 1
bios: ovmf
boot: order=scsi0
cores: 4
cpu: host
efidisk0: local-lvm:vm-103-disk-1,efitype=4m,pre-enrolled-keys=1,size=4M
machine: pc-q35-6.1
memory: 8192
meta: creation-qemu=6.1.1,ctime=1748588970
name: win11
net0: e1000=6E:FA:51:9A:D2:39,bridge=vmbr0,firewall=1
numa: 0
ostype: win11
parent: apps
scsi0: local-lvm:vm-103-disk-0,cache=writeback,size=64G
scsihw: virtio-scsi-pci
smbios1: uuid=194d50cf-8f86-4fa2-b770-28aa88109b43
sockets: 1
tpmstate0: local-lvm:vm-103-disk-2,size=4M,version=v2.0
vga: virtio,memory=64
vmgenid: 5a10564a-ca41-4136-93a9-f3f999390ac4
```

Convert thin-provided disk to qcow2:

```
# dd if=/dev/pve/vm-103-disk-0 of=/tank/win11-20250602.raw bs=4M status=progress
# qemu-img convert -f raw -O qcow2 /tank/win11-20250602.raw /tank/win11-20250602.qcow2
```

Now create the vm **without** specifying the disk image, modifying the MAC addr, and update machine type to latest `pc-q35-9.2+pve1` (will change to `i440fx` shortly after):

```
qm create 100 \
--name "win11" \
--bios ovmf \
--boot order=scsi0 \
--cores 4 \
--cpu host \
--machine  pc-q35-9.2+pve1 \
--memory 8192 \
--net0 e1000=6E:FA:51:9A:D2:40,bridge=vmbr0,firewall=1 \
--numa 0 \
--ostype win11 \
--scsihw virtio-scsi-pci \
--sockets 1 \
--vga virtio,memory=64
```

Note that for NIC choice, using `VirtIO` might be better than `Intel E1000`, but I did not test that.

Then **importing** the qcow2 image file into an existing vm on the new pve host, using `sudo qm importdisk 100 <path-to-qcow2-file> <pve-storage-id>`. 

For example:

- `sudo qm importdisk 100 /mnt/win11-20250602.qcow2 local-lvm`: import to `local-lvm` storage (thin-provisioning);
- `sudo qm importdisk 100 /mnt/win11-20250602.qcow2 local-vm-images`: `local-vm-image` is an added storage by adding the following into `/etc/pve/storage.cfg` (or use `pvesm add dir <STORAGE_ID> --path <PATH>`):

```
dir: local-vm-images
    path /opt/vm-images
    content images,iso
```

As the WebUI does not show the detailed info about `/etc/pve/storage.cfg`, one should inspect the file or use `pvesm status` to check details.

```
$ sudo pvesm status
Name                   Type     Status           Total            Used       Available        %
local                   dir     active        40516856        12633628        25792836   31.18%
local-lvm           lvmthin     active        56545280               0        56545280    0.00%
local-vm-images         dir     active      1967615968       132112976      1735479852    6.71%
```

After importing, the WebUI will show the unused disk for vm 100. One of the two ways to attach it to SCSI bus:
-  WebUI: "Edit" it by assign it as `scsi0` with `cache=writeback` attributes.
-  Cmd line: `sudo qm set 100 --scsi0 local-lvm:vm-100-disk-0,cache=writeback,size=64G`

The end resoult is that:

```
$ sudo qm config 100|grep scsi0
scsi0: local-lvm:vm-100-disk-0,cache=writeback,size=64G
```

Now add both efidisk and tmp from WebUI, making sure that they are `vm-100-disk-1` and  `vm-100-disk-2` respectively.

Now set identical BIOS/VM ids (for keeping the Windows license be still valid in the clone):

```
qm set 100 --smbios1 uuid=194d50cf-8f86-4fa2-b770-28aa88109b43
qm set 100 --vmgenid 5a10564a-ca41-4136-93a9-f3f999390ac4
```

Also enable the guest agent:

```
qm set 100 --agent 1
```

Boot the VM from WebUI to test that everything is working (except the passthrough aspects).

# VM Config for Passthrough

## VBIOS

The VBIOS (Video BIOS) is critical for iGPU passthrough, especially with Intel GPUs, as it provides the firmware needed for proper initialization in the VM. Without a valid VBIOS, you may encounter issues like black screens, invalid PCI ROM header errors (e.g., expecting 0xaa55, got 0xffff), or failure to initialize the GPU in the guest OS.

Instead of extracting VBIOS from firmware, we download the VBIOS ROM from [the web](https://www.123pan.com/s/20P0Vv-d2A6H.html), provided from [this post](https://zhuanlan.zhihu.com/p/704779862). Rename the file as `igpu-uhd630.rom` and put it under `/usr/share/kvm` with `0644` mode.

### FIXME (optional)

The most reliable VBIOS is one extracted from the specific hardware, which matches the iGPU and motherboard firmware. Download firmware package from [hp support](https://support.hp.com/us-en/drivers/swdetails/hp-elitedesk-800-65w-g4-desktop-mini-pc/). The file name is `sp156646.exe`, which contains the firmware `Q21_023000.bin`, which in turn contains `Intel VBIOS 9.2.1014 (2018/06/21)` and `Intel GOP 9.0.1075`.

FIXME: how to extract VBIOS from the firmware package?

## VM Config

The following is a working version of the VM config:

```
# qm config 100
agent: 1
args: -set device.hostpci0.addr=02.0 -set device.hostpci0.x-igd-gms=0x2 -set device.hostpci0.x-igd-opregion=on
bios: ovmf
boot:
cores: 4
cpu: host
efidisk0: local-lvm:vm-100-disk-1,efitype=4m,pre-enrolled-keys=1,size=4M
hostpci0: 0000:00:02,legacy-igd=1,romfile=igpu-uhd630.rom
hostpci1: 0000:00:14.3
machine: pc-i440fx-9.2
memory: 8192
meta: creation-qemu=9.2.0,ctime=1748871264
name: win11
net0: e1000=6E:FA:51:9A:D2:40,bridge=vmbr0,firewall=1
numa: 0
ostype: win11
scsi0: local-lvm:vm-100-disk-0,cache=writeback,size=64G
scsihw: virtio-scsi-pci
smbios1: uuid=194d50cf-8f86-4fa2-b770-28aa88109b43
sockets: 1
tpmstate0: local-lvm:vm-100-disk-2,size=4M,version=v2.0
usb0: host=062a:4101
usb1: host=8087:0aaa
vga: none
vmgenid: 5a10564a-ca41-4136-93a9-f3f999390ac4
```

Brief explanation:

- `bios: ovmf`: Uses UEFI firmware, standard for Windows 11.
- `machine: pc-i440fx-9.2`: Uses the older i440FX chipset instead of Q35 for `legacy-igd`. Not that `pc-i440fx-9.2+pve1` is not working.
- `hostpci0`: Passes the iGPU (0000:00:02.0) with:
    - `legacy-igd=1`: Enables legacy VGA arbitration for Intel integrated GPUs, critical for passthrough.
    - `romfile=igpu-uhd630.rom`: Specifies the VBIOS, with `/usr/share/kvm/` the PVE default path.
- `args`:
    - `set device.hostpci0.addr=02.0`: Remaps the iGPU to PCI address 02.0 in the guest (likely to match Windows expectations).
    - `set device.hostpci0.x-igd-gms=0x2`: Allocates 64 MB of stolen memory (0x2 = 2 * 32 MB) for the iGPU’s Graphics Memory System.
    - `set device.hostpci0.x-igd-opregion=on`: Enables the `OpRegion` for Intel iGPU, necessary for driver initialization.
- `vga: none`: Disables emulated VGA, relying solely on the passed-through iGPU.
- `cpu: host`: Passes host CPU features, good for performance but may expose MSRs (explaining dmesg MSR warnings).
- `usb0: host=062a:4101`: mouse/keyboard
- `usb1: host=8087:0aaa`: Bluetooth

## `dmesg` at VM start

The following is the host `dmesg` output when starting the Windows 11 VM:

```
[  494.126884] tap100i0: entered promiscuous mode
[  494.172975] vmbr0: port 2(fwpr100p0) entered blocking state
[  494.172980] vmbr0: port 2(fwpr100p0) entered disabled state
[  494.172995] fwpr100p0: entered allmulticast mode
[  494.173033] fwpr100p0: entered promiscuous mode
[  494.173080] vmbr0: port 2(fwpr100p0) entered blocking state
[  494.173082] vmbr0: port 2(fwpr100p0) entered forwarding state
[  494.182620] fwbr100i0: port 1(fwln100i0) entered blocking state
[  494.182624] fwbr100i0: port 1(fwln100i0) entered disabled state
[  494.182638] fwln100i0: entered allmulticast mode
[  494.182677] fwln100i0: entered promiscuous mode
[  494.182725] fwbr100i0: port 1(fwln100i0) entered blocking state
[  494.182727] fwbr100i0: port 1(fwln100i0) entered forwarding state
[  494.192365] fwbr100i0: port 2(tap100i0) entered blocking state
[  494.192370] fwbr100i0: port 2(tap100i0) entered disabled state
[  494.192382] tap100i0: entered allmulticast mode
[  494.192443] fwbr100i0: port 2(tap100i0) entered blocking state
[  494.192446] fwbr100i0: port 2(tap100i0) entered forwarding state
[  495.151099] vfio-pci 0000:00:02.0: Invalid PCI ROM header signature: expecting 0xaa55, got 0xa1f9
[  495.151115] vfio-pci 0000:00:02.0: Invalid PCI ROM header signature: expecting 0xaa55, got 0xa1f9
[  495.151144] vfio-pci 0000:00:02.0: Invalid PCI ROM header signature: expecting 0xaa55, got 0xa1f9
[  495.151161] vfio-pci 0000:00:02.0: Invalid PCI ROM header signature: expecting 0xaa55, got 0xa1f9
[  508.622909] usb 1-1: reset full-speed USB device number 2 using xhci_hcd
[  508.942997] usb 1-14: reset full-speed USB device number 3 using xhci_hcd
[  512.330171] kvm: kvm [4638]: ignored rdmsr: 0x1ad data 0x0
[  560.810476] usb 1-14: reset full-speed USB device number 3 using xhci_hcd
```

Brief notes:

- The error report `Invalid PCI ROM header signature: expecting 0xaa55, got 0xa1f9` seems happens before loading the provided `igpu-uhd630.rom`, so it can be ignored.
- The display screen blanks for about 15 seconds. It seems that the iGPU initialization happens betw `495.151161` and `508.622909`, as after that, the display LED turns from red to green, and then Windows UI shows up.
- Append `-trace enable=vfio*,file=/var/log/qemu/100.log` to `args` line for getting some debug info during vm start.
- If also passthrough `0:1f.3` (audio endpoint), then the host network will be broken while the VM still works. The related vm start time `dmesg` (using `journalctl -xb -1` after reboot) shows that `eno1` (`0:1f.6`) was reset and disabled. This suggests that the IOMMU group for `0:1f.*` is hardware-tied somehow, which is different from IOMMU group for `0:14.*` (as the WiFi device `0:14.3` can be passthrough alone to the VM).

    ```
    Jun 03 20:35:58 pve kernel: Deleting MTD partitions on "0000:00:1f.5":
    Jun 03 20:35:58 pve kernel: Deleting BIOS MTD partition
    Jun 03 20:35:58 pve kernel: e1000e 0000:00:1f.6 eno1: removed PHC
    Jun 03 20:35:58 pve kernel: e1000e 0000:00:1f.6 eno1: NIC Link is Down
    Jun 03 20:35:58 pve kernel: vmbr0: port 1(eno1) entered disabled state
    Jun 03 20:35:58 pve kernel: e1000e 0000:00:1f.6 eno1 (unregistering): left allmulticast mode
    Jun 03 20:35:58 pve kernel: e1000e 0000:00:1f.6 eno1 (unregistering): left promiscuous mode
    Jun 03 20:35:58 pve kernel: vmbr0: port 1(eno1) entered disabled state
    ```

# References

- [Grok3](https://x.com/i/grok) or [DeepSeek](https://chat.deepseek.com/): ask them about anything!
- [教程: PVE下uhd630核显直通HDMI输出 以NUC9为例](https://zhuanlan.zhihu.com/p/704779862)
- [Intel Graphics Device (IGD) assignment with vfio-pci](https://github.com/qemu/qemu/blob/master/docs/igd-assign.txt)
- [PVE PCIe Passthrough](https://pve.proxmox.com/wiki/PCI(e)_Passthrough)
- [iGPU Passthrough to VM (Intel Integrated Graphics)](https://3os.org/infrastructure/proxmox/gpu-passthrough/igpu-passthrough-to-vm/)
- [Proxmox VE 8.3: Windows 11 vGPU (VT-d) Passthrough with Intel Alder Lake](https://www.derekseaman.com/2024/07/proxmox-ve-8-2-windows-11-vgpu-vt-d-passthrough-with-intel-alder-lake.html)
- [`q35` issues discussion](https://github.com/gangqizai/igd/issues/1)
- [pve环境10代i5-10400核显直通](https://linkzz.org/posts/pve-igd-passthrough/): using UBU to extract VBIOS from firmware image (in case the firmware image is not recognized by UBU, download one from other manufacturer such as `asrockchina.com.cn` and give it a try).

    ```
                  UBU             EfiRom             rom-parser
    fireware.bin ------> gop.efi ---------> igpu.rom -----------> ok!
                extract          convert              verify
    ```

    - `UBU` can be downloaded following this post on [chiphell.com](https://www.chiphell.com/forum.php?mod=viewthread&tid=2596245)
    - `EfiRom.exe`, and EDKII tool, can be downloaded from [github](https://github.com/tianocore/edk2-BaseTools-win32)
    - `rom-parser` source code can be downloaded from [github](https://github.com/awilliam/rom-parser)
- [Proxmox 5700G APU GPU Passthrough Notes](https://gist.github.com/matt22207/bb1ba1811a08a715e32f106450b0418a)
- [Proxmox - Ryzen 7000 series - AMD Radeon 680M/780M/RDNA2/RDNA3 GPU passthrough](https://github.com/isc30/ryzen-gpu-passthrough-proxmox): VBIOS files are included.