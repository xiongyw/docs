# Background

- Created: 2025.6.6
- Last Update: 2025.6.7

As the [iGPU test with HP EliteDesk 800 G4 DM](https://github.com/xiongyw/docs/blob/master/pve-8.4-1_hp-elitedesk-800-g4-dm.md) seems promising, I switched to a slightly beefier one (`Lenovo M920x Tiny` with `i7-9700` CPU and 64G DDR4), trying to have a similar setup for working environment.

# Host Install

This pc has two m.2 ssd slots:

- slot1: 256G ssd, an existing windows 11, kept as a backup;
- slot2: 1T ssd, to install pve 8.4-1 and VMs;
- BIOS boot order settings: usb, slot2, slot1
    - `usb`: allows boot from install media
    - `slot2`: boot pve by default; in case to boot the native windows on `slot1`, use `efibootmgr -n <id>` to set the next boot choice;
    - `slot1`: last priority to boot the native windows backup;

Install PVE as usual, and after that:

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
- `apt install sudo binutils build-essential git tig htop tmux inxi nmon parted ranger ncdu inxi ripgrep libguestfs-tools vim`
- install linux headers: `apt install pve-headers-$(uname -r)`. headers will be installed under `/usr/src/linux-headers-$(uname -r)` folder. a symlink to it will be created at `/lib/modules/$(uname -r)/build`.
- install linux source: `apt install pve-kernel-$(uname -r)`. kernel source will be installed under `/usr/src/linux-headers-$(uname -r)` folder. a symlink to it will be created at `/lib/modules/$(uname -r)/build`.

- remove subscription popup: `sed -i.bak "s/data.status !== 'Active'/false/g" /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js && systemctl restart pveproxy.service`
- [install `netbird`](https://docs.netbird.io/how-to/installation), by `curl -fsSL https://pkgs.netbird.io/install.sh | sh`.

- Remove `local-lvm` and expand `local`:

    - Default config:

        ```
        root@m920x-pve:~# cat /etc/pve/storage.cfg
        dir: local
                path /var/lib/vz
                content iso,vztmpl,backup

        lvmthin: local-lvm
                thinpool data
                vgname pve
                content rootdir,images

        root@m920x-pve:~# pvesm status
        Name             Type     Status           Total            Used       Available        %
        local             dir     active        98497780         4546092        88902140    4.62%
        local-lvm     lvmthin     active       855855104               0       855855104    0.00%

        root@m920x-pve:~# lsblk
        NAME               MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
        nvme1n1            259:0    0 953.9G  0 disk
        ├─nvme1n1p1        259:1    0  1007K  0 part
        ├─nvme1n1p2        259:2    0     1G  0 part /boot/efi
        └─nvme1n1p3        259:3    0 952.9G  0 part
          ├─pve-swap       252:0    0     8G  0 lvm  [SWAP]
          ├─pve-root       252:1    0    96G  0 lvm  /
          ├─pve-data_tmeta 252:2    0   8.3G  0 lvm
          │ └─pve-data     252:4    0 816.2G  0 lvm
          └─pve-data_tdata 252:3    0 816.2G  0 lvm
            └─pve-data     252:4    0 816.2G  0 lvm
        nvme0n1            259:4    0 238.5G  0 disk
        ├─nvme0n1p1        259:5    0   300M  0 part
        └─nvme0n1p2        259:6    0 238.2G  0 part

        root@m920x-pve:~# lvscan
          ACTIVE            '/dev/pve/data' [<816.21 GiB] inherit
          ACTIVE            '/dev/pve/swap' [8.00 GiB] inherit
          ACTIVE            '/dev/pve/root' [96.00 GiB] inherit

        root@m920x-pve:~# lvs -a
          LV              VG  Attr       LSize    Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
          data            pve twi-a-tz-- <816.21g             0.00   0.23
          [data_tdata]    pve Twi-ao---- <816.21g
          [data_tmeta]    pve ewi-ao----   <8.33g
          [lvol0_pmspare] pve ewi-------   <8.33g
          root            pve -wi-ao----   96.00g
          swap            pve -wi-ao----    8.00g

        ```

    - Remove `local-lvm`: using WebGUI, go to `Datacenter`, click storage and select local-lvm. 'Remove' button. Or:

        ```
        root@m920x-pve:~# pvesm remove local-lvm
        root@m920x-pve:~# pvesm status
        Name         Type     Status           Total            Used       Available        %
        local         dir     active        98497780         4546324        88901908    4.62%

        root@m920x-pve:~# cat /etc/pve/storage.cfg
        dir: local
                path /var/lib/vz
                content vztmpl,iso,backup
        ```
    - Add `rootdir,images` content type to `local` (or directly edit `/etc/pve/storage.cfg`):

        ```
        root@m920x-pve:~# pvesm set local --content iso,vztmpl,backup,rootdir,images
        root@m920x-pve:~# cat /etc/pve/storage.cfg
        dir: local
                path /var/lib/vz
                content backup,images,vztmpl,rootdir,iso
        ```

    - remove swap and `/dev/pve/swap`:

        ```
        root@m920x-pve:~# free
                      total        used        free      shared  buff/cache   available
        Mem:        65678776     2078912    63923316       48484      346836    63599864
        Swap:        8388604           0     8388604
        root@m920x-pve:~# swapoff -a
        root@m920x-pve:~# free
                      total        used        free      shared  buff/cache   available
        Mem:        65678776     2070776    63931368       48492      347012    63608000
        Swap:              0           0           0

        root@m920x-pve:~# cat /etc/fstab
        # <file system> <mount point> <type> <options> <dump> <pass>
        /dev/pve/root / ext4 errors=remount-ro 0 1
        UUID=7CE8-8954 /boot/efi vfat defaults 0 1
        /dev/pve/swap none swap sw 0 0
        proc /proc proc defaults 0 0
        
        root@m920x-pve:~# sed -i '/swap/d' /etc/fstab
        
        root@m920x-pve:~# cat /etc/fstab
        # <file system> <mount point> <type> <options> <dump> <pass>
        /dev/pve/root / ext4 errors=remount-ro 0 1
        UUID=7CE8-8954 /boot/efi vfat defaults 0 1
        proc /proc proc defaults 0 0

        root@m920x-pve:~# lvremove /dev/pve/swap
        Do you really want to remove active logical volume pve/swap? [y/n]: y
          Logical volume "swap" successfully removed.
        
        root@m920x-pve:~# lvscan
          ACTIVE            '/dev/pve/data' [<816.21 GiB] inherit
          ACTIVE            '/dev/pve/root' [96.00 GiB] inherit
        ```
    - remove `/dev/pve/data`:

        ```
        root@m920x-pve:~# lvremove /dev/pve/data
        Do you really want to remove active logical volume pve/data? [y/n]: y
          Logical volume "data" successfully removed.
        root@m920x-pve:~# lvscan
          ACTIVE            '/dev/pve/root' [96.00 GiB] inherit

        root@m920x-pve:~# lsblk
        NAME         MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
        nvme1n1      259:0    0 953.9G  0 disk
        ├─nvme1n1p1  259:1    0  1007K  0 part
        ├─nvme1n1p2  259:2    0     1G  0 part /boot/efi
        └─nvme1n1p3  259:3    0 952.9G  0 part
          └─pve-root 252:1    0    96G  0 lvm  /
        nvme0n1      259:4    0 238.5G  0 disk
        ├─nvme0n1p1  259:5    0   300M  0 part
        └─nvme0n1p2  259:6    0 238.2G  0 part
        ```
    - resize `/dev/pve/root` to take all free space:

        ```
        root@m920x-pve:~# lvresize -l +100%FREE /dev/pve/root
          Size of logical volume pve/root changed from 96.00 GiB (24576 extents) to <952.87 GiB (243934 extents).
          Logical volume pve/root successfully resized.
        root@m920x-pve:~# lsblk
        NAME         MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
        nvme1n1      259:0    0 953.9G  0 disk
        ├─nvme1n1p1  259:1    0  1007K  0 part
        ├─nvme1n1p2  259:2    0     1G  0 part /boot/efi
        └─nvme1n1p3  259:3    0 952.9G  0 part
          └─pve-root 252:1    0 952.9G  0 lvm  /
        nvme0n1      259:4    0 238.5G  0 disk
        ├─nvme0n1p1  259:5    0   300M  0 part
        └─nvme0n1p2  259:6    0 238.2G  0 part
        
        root@m920x-pve:~# resize2fs /dev/pve/root
        resize2fs 1.47.0 (5-Feb-2023)
        Filesystem at /dev/pve/root is mounted on /; on-line resizing required
        old_desc_blocks = 12, new_desc_blocks = 120
        The filesystem on /dev/pve/root is now 249788416 (4k) blocks long.

        root@m920x-pve:~# df -h /
        Filesystem            Size  Used Avail Use% Mounted on
        /dev/mapper/pve-root  938G  4.4G  894G   1% /
        ```

- Shrink `/dev/pve/root` and recreate a small-sized thinpool `/dev/pve/data`: the original idea is to put all space to `/dev/pve/root` for simplicity, but later it turns out that for windows vm, the TPM storage does not support `.qcow2` yet, it can only be `raw` format on `/dev/pve/root`, and `raw` format disk does not support snapshot, which means the the whole VM does not support snapshot. That's the reason for recreating a small thinpool for storing TPM (efidisk and windows disk can be using `qcow2` format on `/dev/pve/root`). Two references:

    - [raw does not support snapshot](https://forum.proxmox.com/threads/the-current-guest-configuration-does-not-support-taking-new-snapshots.73944/post-330534)
    - [TPM only supports raw for now](https://forum.proxmox.com/threads/does-tpm-disk-affect-snapshot-support-cannot-take-snapshot.103558/)

- At this point, the ip addr are `192.168.10.119/24` (for `eno1` via DHCP) and `100.102.133.92/16` (static address for `wt0` created by [netbird](https://netbird.io/)), and we have:

    ```
    root@m920x-pve:~# inxi -b
    System:
      Host: m920x-pve Kernel: 6.8.12-11-pve arch: x86_64 bits: 64 Console: pty pts/1 Distro: Debian
        GNU/Linux 12 (bookworm)
    Machine:
      Type: Mini-pc System: LENOVO product: 10S4S00M00 v: ThinkCentre M920x-N000 serial: M70B79AE
      Mobo: LENOVO model: 3135 v: NOK serial: N/A UEFI: LENOVO v: M1UKT72A date: 06/12/2023
    CPU:
      Info: 8-core Intel Core i7-9700 [MCP] speed (MHz): avg: 1767 min/max: 800/4700
    Graphics:
      Device-1: Intel CoffeeLake-S GT2 [UHD Graphics 630] driver: i915 v: kernel
      Display: server: No display server data found. Headless machine? tty: 164x69
        resolution: 1280x1024
      API: OpenGL Message: GL data unavailable in console for root.
    Network:
      Device-1: Intel Ethernet I219-LM driver: e1000e
    Drives:
      Local Storage: total: 1.16 TiB used: 4.39 GiB (0.4%)
    Info:
      Processes: 208 Uptime: 7m Memory: 62.64 GiB used: 2.01 GiB (3.2%) Init: systemd
      target: graphical (5) Shell: Bash inxi: 3.3.26

    root@m920x-pve:~# uname -a
    Linux m920x-pve 6.8.12-11-pve #1 SMP PREEMPT_DYNAMIC PMX 6.8.12-11 (2025-05-22T09:39Z) x86_64 GNU/Linux
    root@m920x-pve:~# cat /proc/fb
    0 i915drmfb
    root@m920x-pve:~# cat /etc/network/interfaces
    auto lo
    iface lo inet loopback
    iface eno1 inet manual
    auto vmbr0
    iface vmbr0 inet static
            address 192.168.10.119/24
            gateway 192.168.10.1
            bridge-ports eno1
            bridge-stp off
            bridge-fd 0
    source /etc/network/interfaces.d/*

    root@m920x-pve:~# lsblk
    NAME                         MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
    nvme0n1                      259:0    0 953.9G  0 disk
    ├─nvme0n1p1                  259:2    0  1007K  0 part
    ├─nvme0n1p2                  259:3    0     1G  0 part /boot/efi
    └─nvme0n1p3                  259:4    0 952.9G  0 part
      ├─pve-root                 252:0    0 800.9G  0 lvm  /
      ├─pve-data_tmeta           252:1    0    76M  0 lvm
      │ └─pve-data-tpool         252:3    0   150G  0 lvm
      │   ├─pve-data             252:4    0   150G  1 lvm
      │   └─pve-vm--100--disk--0 252:5    0     4M  0 lvm
      └─pve-data_tdata           252:2    0   150G  0 lvm
        └─pve-data-tpool         252:3    0   150G  0 lvm
          ├─pve-data             252:4    0   150G  1 lvm
          └─pve-vm--100--disk--0 252:5    0     4M  0 lvm
    nvme1n1                      259:1    0 238.5G  0 disk
    ├─nvme1n1p1                  259:5    0   300M  0 part
    └─nvme1n1p2                  259:6    0 238.2G  0 part

    root@m920x-pve:~# lvscan
      ACTIVE            '/dev/pve/data' [150.00 GiB] inherit
      ACTIVE            '/dev/pve/root' [<800.87 GiB] inherit
      ACTIVE            '/dev/pve/vm-100-disk-0' [4.00 MiB] inherit
    root@m920x-pve:~# lvs
      LV            VG  Attr       LSize    Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
      data          pve twi-aotz--  150.00g             0.01   10.44
      root          pve -wi-ao---- <800.87g
      vm-100-disk-0 pve Vwi-aotz--    4.00m data        3.12

    root@m920x-pve:~# free
                  total        used        free      shared  buff/cache   available
    Mem:        65678776     2050808    63844660       48256      445864    63627968
    Swap:              0           0           0

    root@m920x-pve:~# lspci -tvnn
    -[0000:00]-+-00.0  Intel Corporation 8th/9th Gen Core 8-core Desktop Processor Host Bridge/DRAM Registers [Coffee Lake S] [8086:3e30]
              +-02.0  Intel Corporation CoffeeLake-S GT2 [UHD Graphics 630] [8086:3e98]
              +-08.0  Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th/8th Gen Core Processor Gaussian Mixture Model [8086:1911]
              +-14.0  Intel Corporation Cannon Lake PCH USB 3.1 xHCI Host Controller [8086:a36d]
              +-14.2  Intel Corporation Cannon Lake PCH Shared SRAM [8086:a36f]
              +-16.0  Intel Corporation Cannon Lake PCH HECI Controller [8086:a360]
              +-16.3  Intel Corporation Cannon Lake PCH Active Management Technology - SOL [8086:a363]
              +-17.0  Intel Corporation Cannon Lake PCH SATA AHCI Controller [8086:a352]
              +-1b.0-[01]----00.0  MAXIO Technology (Hangzhou) Ltd. NVMe SSD Controller MAP1202 [1e4b:1202]
              +-1b.4-[02]----00.0  Sandisk Corp WD Black SN750 / PC SN730 NVMe SSD [15b7:5006]
              +-1d.0-[03-6d]--
              +-1f.0  Intel Corporation Q370 Chipset LPC/eSPI Controller [8086:a306]
              +-1f.3  Intel Corporation Cannon Lake PCH cAVS [8086:a348]
              +-1f.4  Intel Corporation Cannon Lake PCH SMBus Controller [8086:a323]
              +-1f.5  Intel Corporation Cannon Lake PCH SPI Controller [8086:a324]
              \-1f.6  Intel Corporation Ethernet Connection (7) I219-LM [8086:15bb]

    root@m920x-pve:~# find /sys/kernel/iommu_groups/ -type l |sort
    /sys/kernel/iommu_groups/0/devices/0000:00:02.0
    /sys/kernel/iommu_groups/10/devices/0000:01:00.0
    /sys/kernel/iommu_groups/11/devices/0000:02:00.0
    /sys/kernel/iommu_groups/1/devices/0000:00:00.0
    /sys/kernel/iommu_groups/2/devices/0000:00:08.0
    /sys/kernel/iommu_groups/3/devices/0000:00:14.0
    /sys/kernel/iommu_groups/3/devices/0000:00:14.2
    /sys/kernel/iommu_groups/4/devices/0000:00:16.0
    /sys/kernel/iommu_groups/4/devices/0000:00:16.3
    /sys/kernel/iommu_groups/5/devices/0000:00:17.0
    /sys/kernel/iommu_groups/6/devices/0000:00:1b.0
    /sys/kernel/iommu_groups/7/devices/0000:00:1b.4
    /sys/kernel/iommu_groups/8/devices/0000:00:1d.0
    /sys/kernel/iommu_groups/9/devices/0000:00:1f.0
    /sys/kernel/iommu_groups/9/devices/0000:00:1f.3
    /sys/kernel/iommu_groups/9/devices/0000:00:1f.4
    /sys/kernel/iommu_groups/9/devices/0000:00:1f.5
    /sys/kernel/iommu_groups/9/devices/0000:00:1f.6

    root@m920x-pve:~# lsusb -tv
    /:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=xhci_hcd/10p, 10000M
        ID 1d6b:0003 Linux Foundation 3.0 root hub
        |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 5000M
            ID 05e3:0626 Genesys Logic, Inc. Hub
    /:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=xhci_hcd/16p, 480M
        ID 1d6b:0002 Linux Foundation 2.0 root hub
        |__ Port 2: Dev 2, If 0, Class=Hub, Driver=hub/4p, 480M
            ID 05e3:0610 Genesys Logic, Inc. Hub
            |__ Port 1: Dev 3, If 0, Class=Human Interface Device, Driver=usbhid, 12M
                ID 062a:4101 MosArt Semiconductor Corp. Wireless Keyboard/Mouse
            |__ Port 1: Dev 3, If 1, Class=Human Interface Device, Driver=usbhid, 12M
                ID 062a:4101 MosArt Semiconductor Corp. Wireless Keyboard/Mouse

    root@m920x-pve:~# efibootmgr
    BootCurrent: 0000
    Timeout: 2 seconds
    BootOrder: 0000,000C,0001,0004,0002,0003
    Boot0000* proxmox
    Boot0001* Windows Boot Manager
    Boot0002* CD/DVD Device
    Boot0003* McAfee Opal Compatibility Check
    Boot0004* Generic Usb Device
    Boot000C* UEFI OS
    ```


# Host Config for Passthrough

- Assuming `vt-d` is already enabled in BIOS.

    ```
    root@m920x-pve:~# dmesg|grep -i vt-d
    [    3.282643] i915 0000:00:02.0: [drm] VT-d active for gfx access
    ```

- Enable iommu via `grub cmdline`:

    - Edit `/etc/default/grub`: `GRUB_CMDLINE_LINUX_DEFAULT` to enable iommu and passthrough:

      ```
      GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on iommu=pt"
      ```

    - Run `update-grub`: use `grep iommo /boot/grub/grub.cfg` to confirm the updates.

- Split each physical function in `0:1f.*` into different IOMMU group:

    ```
    # crontab -l
    @reboot /root/passthrough-tweak.sh

    cat /root/passthrough-tweak.sh
    #!/usr/bin/bash

    #
    # put `0:1f.*` into separate iommu groups
    #
    echo 1 > /sys/bus/pci/devices/0000\:00\:1f.0/remove
    echo 1 > /sys/bus/pci/devices/0000\:00\:1f.3/remove
    echo 1 > /sys/bus/pci/devices/0000\:00\:1f.4/remove
    echo 1 > /sys/bus/pci/devices/0000\:00\:1f.5/remove
    echo 1 > /sys/bus/pci/devices/0000\:00\:1f.6/remove
    echo 1 > /sys/bus/pci/rescan

    #
    # `0:1f.6` is NIC. Need restart networking
    #
    systemctl restart networking
    systemctl restart netbird

    sleep 10
    ```
- Enforce kernel modules binding:
    - Edit `/etc/modules`, add the following for loading these modules by default:

        ```
        vfio
        vfio_iommu_type1
        vfio_pci
        vfio_virqfd
        ```

    - Add `/etc/modprobe.d/passthrough.conf`, with the following content:

        ```
        # don't load driver for iGPU and sound card
        blacklist i915
        blacklist snd_hda_intel
        blacklist snd_sof_pci_intel_cnl

        # load vfio-pci driver instead
        options vfio-pci ids=8086:3e98,8086:a348

        #
        options vfio_iommu_type1 allow_unsafe_interrupts=1

        # tell VMs to ignore access to MSRs (Model-Specific Registers)
        options kvm ignore_msrs=1
        ```

    - Run `update-initramfs -u -k all` to update initramfs accordingly for all kernels.

- Reboot the host, now the display should freeze around `/dev/mapper/pve-root: clean ...`. SSH to the host and check that IOMMU is enabled, and both iGPU ()`0:2.0`) and sound card (`0:1f.3`) are in their separate IOMMU groups (and bound to `vfio_pci` driver):

    ```
    root@m920x-pve:~# find /sys/kernel/iommu_groups/ -type l |sort
    /sys/kernel/iommu_groups/0/devices/0000:00:02.0
    /sys/kernel/iommu_groups/10/devices/0000:01:00.0
    /sys/kernel/iommu_groups/11/devices/0000:02:00.0
    /sys/kernel/iommu_groups/12/devices/0000:00:1f.3
    /sys/kernel/iommu_groups/13/devices/0000:00:1f.4
    /sys/kernel/iommu_groups/14/devices/0000:00:1f.5
    /sys/kernel/iommu_groups/15/devices/0000:00:1f.6
    /sys/kernel/iommu_groups/1/devices/0000:00:00.0
    /sys/kernel/iommu_groups/2/devices/0000:00:08.0
    /sys/kernel/iommu_groups/3/devices/0000:00:14.0
    /sys/kernel/iommu_groups/3/devices/0000:00:14.2
    /sys/kernel/iommu_groups/4/devices/0000:00:16.0
    /sys/kernel/iommu_groups/4/devices/0000:00:16.3
    /sys/kernel/iommu_groups/5/devices/0000:00:17.0
    /sys/kernel/iommu_groups/6/devices/0000:00:1b.0
    /sys/kernel/iommu_groups/7/devices/0000:00:1b.4
    /sys/kernel/iommu_groups/8/devices/0000:00:1d.0
    /sys/kernel/iommu_groups/9/devices/0000:00:1f.0

    root@m920x-pve:~# dmesg|grep  "00:02.0:"
    [    0.461711] pci 0000:00:02.0: [8086:3e98] type 00 class 0x030000 PCIe Root Complex Integrated Endpoint
    [    0.461726] pci 0000:00:02.0: BAR 0 [mem 0xcb000000-0xcbffffff 64bit]
    [    0.461729] pci 0000:00:02.0: BAR 2 [mem 0x40000000-0x4fffffff 64bit pref]
    [    0.461731] pci 0000:00:02.0: BAR 4 [io  0x3000-0x303f]
    [    0.461743] pci 0000:00:02.0: Video device with shadowed ROM at [mem 0x000c0000-0x000dffff]
    [    0.488483] pci 0000:00:02.0: vgaarb: setting as boot VGA device
    [    0.488483] pci 0000:00:02.0: vgaarb: bridge control possible
    [    0.488483] pci 0000:00:02.0: vgaarb: VGA device added: decodes=io+mem,owns=io+mem,locks=none
    [    0.518702] pci 0000:00:02.0: Adding to iommu group 0
    [    1.998501] vfio-pci 0000:00:02.0: vgaarb: deactivate vga console
    [    1.998504] vfio-pci 0000:00:02.0: vgaarb: VGA decodes changed: olddecodes=io+mem,decodes=io+mem:owns=io+mem

    root@m920x-pve:~# dmesg|grep  "00:1f.3:"
    [    0.468562] pci 0000:00:1f.3: [8086:a348] type 00 class 0x040380 conventional PCI endpoint
    [    0.468633] pci 0000:00:1f.3: BAR 0 [mem 0xcc330000-0xcc333fff 64bit]
    [    0.468643] pci 0000:00:1f.3: BAR 4 [mem 0xcc000000-0xcc0fffff 64bit]
    [    0.468710] pci 0000:00:1f.3: PME# supported from D3hot D3cold
    [    0.518865] pci 0000:00:1f.3: Adding to iommu group 9
    [    5.896168] pci 0000:00:1f.3: [8086:a348] type 00 class 0x040380 conventional PCI endpoint
    [    5.896255] pci 0000:00:1f.3: BAR 0 [mem 0xcc330000-0xcc333fff 64bit]
    [    5.896263] pci 0000:00:1f.3: BAR 4 [mem 0xcc000000-0xcc0fffff 64bit]
    [    5.896329] pci 0000:00:1f.3: PME# supported from D3hot D3cold
    [    5.899262] pci 0000:00:1f.3: Adding to iommu group 12
    [    5.900156] pci 0000:00:1f.3: BAR 4 [mem 0x3f800000-0x3f8fffff 64bit]: assigned
    [    5.900176] pci 0000:00:1f.3: BAR 0 [mem 0x3f920000-0x3f923fff 64bit]: assigned

    root@m920x-pve:~# lspci -s 0:2.0 -vv|grep Kernel
            Kernel driver in use: vfio-pci
            Kernel modules: i915
    root@m920x-pve:~# lspci -s 0:1f.3 -vv|grep Kernel
            Kernel driver in use: vfio-pci
            Kernel modules: snd_hda_intel, snd_sof_pci_intel_cnl

    root@m920x-pve:~# lsmod|grep i915
    root@m920x-pve:~# lsmod|grep snd
    root@m920x-pve:~# cat /proc/fb
    ```

# VM Creation

- Create a VM without specifying the disks yet:

    ```
    root@m920x-pve:~# qm create 100 \
    --agent 1 \
    --name "win11-1" \
    --bios ovmf \
    --boot order=scsi0 \
    --cores 8 \
    --cpu host \
    --machine pc-i440fx-9.2 \
    --memory 32768 \
    --net0 virtio=6E:FA:51:9A:D2:41,bridge=vmbr0,firewall=1 \
    --numa 0 \
    --ostype win11 \
    --scsihw virtio-scsi-pci \
    --sockets 1 \
    --vga virtio,memory=64

    root@m920x-pve:~# qm list
          VMID NAME                 STATUS     MEM(MB)    BOOTDISK(GB) PID
          100 win11-1              stopped    32768              0.00 0
    ```

- disk for windows 11:
    - get a raw disk from a Win11 VM on another pve host:

        ```
        # dd if=/dev/pve/vm-100-disk-0 of=win11-20250606.raw bs=4M status=progress
        ```

    - import the raw disk file to the VM:

        ```
        # qm importdisk 100 ./win11-20250606.raw local
        importing disk './win11-20250606.raw' to VM 100 ...
        Formatting '/var/lib/vz/images/100/vm-100-disk-0.raw', fmt=raw size=68719476736 preallocation=off
        transferred 0.0 B of 64.0 GiB (0.00%)
        transferred 655.4 MiB of 64.0 GiB (1.00%)
        transferred 1.3 GiB of 64.0 GiB (2.00%)
        transferred 1.9 GiB of 64.0 GiB (3.00%)
        ...
        transferred 64.0 GiB of 64.0 GiB (100.00%)
        transferred 64.0 GiB of 64.0 GiB (100.00%)
        unused0: successfully imported disk 'local:100/vm-100-disk-0.raw'
        ```

    - for supporting snapshot, convert raw to qcow2 from WebUI: DiskAction -> Move Storage -> Format: qcow2

    - from WebUI: `Edit` the `unused0` disk in WebUI, attach it to the SCSI controller, and enable "writeback".

- Add `EFI Disk` and `TPM State`, using `local-lvm` storage, for supporting snapshot.

- set identical BIOS/VM ids (for keeping the Windows license be still valid in the clone):

    ```
    qm set 100 --smbios1 uuid=194d50cf-8f86-4fa2-b770-28aa88109b43
    qm set 100 --vmgenid 5a10564a-ca41-4136-93a9-f3f999390ac4
    ```

- At this point, the VM config looks like below, make sure it can boot correcting in WebUI (rename the VM, reinstall netbird):

    ```
    # qm config 100
    agent: 1
    bios: ovmf
    boot: order=scsi0
    cores: 8
    cpu: host
    efidisk0: local-lvm:vm-100-disk-0,efitype=4m,pre-enrolled-keys=1,size=4M
    machine: pc-i440fx-9.2
    memory: 32768
    meta: creation-qemu=9.2.0,ctime=1749196405
    name: win11-1
    net0: virtio=6E:FA:51:9A:D2:41,bridge=vmbr0,firewall=1
    numa: 0
    ostype: win11
    scsi0: local:100/vm-100-disk-3.qcow2,cache=writeback,size=64G,ssd=1
    scsihw: virtio-scsi-pci
    smbios1: uuid=194d50cf-8f86-4fa2-b770-28aa88109b43
    sockets: 1
    tpmstate0: local-lvm:vm-100-disk-1,size=4M,version=v2.0
    vga: virtio,memory=64
    vmgenid: 5a10564a-ca41-4136-93a9-f3f999390ac4
    ```

- Take a snapshot `before-igpu-passthrough` of the VM.

# VM Config for Passthrough

- prepare vbios: copy the vbios file `igpu-uhd630.rom` to `/usr/share/kvm/`;
- add pci devices (iGPU and Audio card) to the VM:
    ```
    hostpci0: 0000:00:02,legacy-igd=1,romfile=igpu-uhd630.rom
    hostpci1: 0000:00:1f.3
    ```
- add usb devices (mouse/keyboard/printer) to the VM:

    ```
    usb0: host=046d:c542        <-- logitech M185
    usb1: host=3554:fc03        <-- ikbc w200 
    usb2: host=062a:4101        <-- ifound mouse/keyboard combo
    usb3: host=0050:0192        <-- fuji m228db printer
    ```

- set `args` for the VM:

    ```
    args: -set device.hostpci0.addr=02.0 -set device.hostpci0.x-igd-gms=0x2 -set device.hostpci0.x-igd-opregion=on
    ```

- change `vga` to `none`: `vga: none`

At this point, iGPU passthrough to Window11 VM should work. Take a snapshot `after-igpu-passthrough`, just in case.

# Final Notes

- Later I need to increase the disk size from 64G to 128G. It takes two steps:
    - Resize the HDD from WebUI, this is easy.
    - Resize the NTFS partition to use the unallocated 64G, this is a bit treaky since between the NTFS partition and the unallocated space, there is a ~700M recovery partition, thus Windows disk manager can not directly extend the NTFS. We need to move the recovery patition to the end of the disk, somehow. As indicated [here](https://forum.proxmox.com/threads/increase-disk-size-on-windows-vm.122268/post-674869), the [MiniTool Partition Wizard Free](https://de.minitool.com/downloadcenter/) can do this while the VM is running (👍). After that, using Windows Disk Manager GUI to exend the NTFS partition.
    - The final VM config looks like this:

        ```
        # qm config 100
        agent: 1
        args: -set device.hostpci0.addr=02.0 -set device.hostpci0.x-igd-gms=0x2 -set device.hostpci0.x-igd-opregion=on
        bios: ovmf
        boot: order=scsi0
        cores: 8
        cpu: host
        efidisk0: local-lvm:vm-100-disk-0,efitype=4m,pre-enrolled-keys=1,size=4M
        hostpci0: 0000:00:02,legacy-igd=1,romfile=igpu-uhd630.rom
        hostpci1: 0000:00:1f.3
        machine: pc-i440fx-9.2
        memory: 32768
        meta: creation-qemu=9.2.0,ctime=1749196405
        name: win11-1
        net0: virtio=6E:FA:51:9A:D2:41,bridge=vmbr0,firewall=1
        numa: 0
        onboot: 1
        ostype: win11
        parent: smart-sound-tech-driver
        scsi0: local:100/vm-100-disk-3.qcow2,cache=writeback,size=128G,ssd=1
        scsihw: virtio-scsi-pci
        smbios1: uuid=194d50cf-8f86-4fa2-b770-28aa88109b43
        sockets: 1
        tpmstate0: local-lvm:vm-100-disk-1,size=4M,version=v2.0
        usb0: host=046d:c542
        usb1: host=3554:fc03
        usb2: host=062a:4101
        usb3: host=0050:0192
        vga: none
        vmgenid: 5a10564a-ca41-4136-93a9-f3f999390ac4
        ```

- The audio transmission via DP port issue as [discussed before](https://github.com/xiongyw/docs/blob/master/pve-8.4-1_hp-elitedesk-800-g4-dm.md) persists. However, as M920x also comes with a HDMI port, I switched from DP to HDMI port to see if there is any difference. It turns out that using HDMI port, Windows 11 device manager reports that there are some audio devices without proper drivers. Installing Q370 chipset driver from Intel does not help. As the last resort (to me it's a kind of bloatware I will uninstall afterwards), I installed [ludashi](https://www.ludashi.com/), which has a feature to automatically search and install drivers for Windows. Although it reports that it cannot identify the type of the audio device, it installed several drivers (Intel and Realtek Smart Sound Technology drivers) for me. After that, Windows device manager is happy, and the audio via HDMI seems working flawlessly, even after reboot several times from Windows itself (😊).
    - TODO: with audio driver installed, check DP output again.