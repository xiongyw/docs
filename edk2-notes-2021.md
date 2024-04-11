# EDK2

The topic can be divided into 4 parts:

- background
    - the need for uefi (wrt legacy bios)
    - triangle-relation among chip-vendors/ibvs/odms
        - https://zhuanlan.zhihu.com/p/83039006
        - MyCorp's position in the ecosystem
    - dtb vs acpi: linux/arm vs windows/x86; arm's sbbr.
    - fsp vs full-open-source firmware
    - uefi competiters: SBL (Slim BootLoader), MinPlatform
        - LinuxBoot, CoreBoot, U-boot
    - ibvs: ami, phoenix, insyde, baiao, kunlun, etc
- uefi/pi/acpi
    - specs
    - books: "beyond bios"
    - articles/ppts
- edk2 implementation specifics
    - tianocore repos
    - intel/ms: guid/com/pe/coff/sln/proj/camel
    - docs: build specs, coding std, file formats, repo/directory structures
    - driver/app write guide
    - porting guide w/ minimal features
    - emulators (host/qemu/fvp/etc)
    - debugging techniques
- linux (arm64)
    - boot protocol
    - efi_stub

Related acronyms: EFI, UEFI, PI, EDK, EDK2, Tiano, ACPI, AML, OSPM, FDT, PSCI, SBSA, SBBR, EBBR, ServerReady, cloud-native, SMBios, FWTS, RAS, CSM, DXE, MDE, TSL, PEI, HOB, DXE, FD, FFS, PCD, VPD, DSC, DEC, INF, FDF, PEIM, PPI, FSP, ASL...

References:

- [BIOSer必读：Intel的下一代BIOS标准USF](https://zhuanlan.zhihu.com/p/443610480)
- [EDK2 official website](https://www.tianocore.org/)
- [EDK2 on Wikipedia](https://en.wikipedia.org/wiki/TianoCore_EDK_II)
- [EDK2 documents](https://github.com/tianocore/tianocore.github.io/wiki/EDK-II-Documents)
- [X86生态圈](https://zhuanlan.zhihu.com/p/83039006)
- [Standards in Arm space (part I)](https://marcin.juszkiewicz.com.pl/2020/10/12/standards-in-arm-space-part-i/)
- [ARM involvment in 4 open source firmware: TF-A, TF-M, EDK2, SCP](https://developer.arm.com/tools-and-software/open-source-software/firmware)
- [ARM and EDK2](https://developer.arm.com/tools-and-software/open-source-software/firmware/edkii-uefi-firmware)
- [UEFI on Wikipedia](https://en.wikipedia.org/wiki/Unified_Extensible_Firmware_Interface)
- [UEFI PI](https://github.com/tianocore/tianocore.github.io/wiki/PI)
- [UEFI/PI FAQ](https://github.com/tianocore/tianocore.github.io/wiki/UEFI-PI_FAQ)
- [UEFI intro](https://www.thomas-krenn.com/en/wiki/Introduction_to_the_Unified_Extensible_Firmware_Interface)
- [Intel IDF2010 presentation](https://www.intel.com/content/dam/doc/guide/efi-development-kit-uefi-advanced-development-innovation.pdf)
- [System Management BIOS](https://en.wikipedia.org/wiki/System_Management_BIOS)
- [ARM SystemReady](https://developer.arm.com/architectures/system-architectures/arm-systemready)
- [Server Base System Architecture](https://en.wikipedia.org/wiki/Server_Base_System_Architecture)
- [SBBR for Pi4B](https://www.hackster.io/news/raspberry-pi-4-strides-towards-serverready-status-via-sbbr-compliant-uefi-firmware-effort-a6e390d5f019)
- [Making Pi ServerReady](https://rpi4-uefi.dev/)
- [enterprise-class vs cloud-native processors](https://www.eetimes.eu/cloud-native-processors-for-a-cloud-native-world/)
- [RPi3 ATF + UEFI implementation](https://github.com/andreiw/RaspberryPiPkg)
- [NV BlueField: ATF+UEFI](https://docs.mellanox.com/display/BlueFieldSWv31011424/Installation+and+Initialization)
- [debug dsdt ssdt with acpica utilities](https://ubuntu.com/blog/debug-dsdt-ssdt-with-acpica-utilities): `sudo acpidump > acpi.out; acpixtract -a acpi.out; iasl -d *.dat`
- FVP related:
    - [FVP download](https://developer.arm.com/tools-and-software/simulation-models/fixed-virtual-platforms)
    - [edk2: ArmPlatformPkg AArch64](https://github.com/tianocore/tianocore.github.io/wiki/ArmPlatformPkg-AArch64)
    - [QEMU and FVP models difference](https://stackoverflow.com/questions/53559478/qemu-and-fvp-models-difference)
- ACPI related:
    - [ACPI与UEFI](https://zhuanlan.zhihu.com/p/25893464)
    - [UEFI vs ACPI/SMBios](https://stackoverflow.com/questions/66603762/does-uefi-replace-standards-like-smbios-and-acpi)
    - [why ACPI on ARM](http://www.secretlab.ca/archives/151)
    - [ARM, SBSA, UEFI, and ACPI](https://lwn.net/Articles/584123/)
    - [ACPI on ARMv8 Servers](https://www.kernel.org/doc/Documentation/arm64/arm-acpi.txt)
    - [AML and ASL](https://wiki.osdev.org/AML)
- [EDK2 repositories](https://developer.arm.com/documentation/102571/0100/Set-up-the-development-environment):
    - [EDK2 main repo](https://github.com/tianocore/edk2):  contains the firmware development environment and required packages for building the UEFI firmware.
    - [EDK2 platform repo](https://github.com/tianocore/edk2-platforms.git): contains the platform workspace and associated modules.
    - [ACPI Component Architecture](https://github.com/acpica/acpica):  provides an open-source implementation of the iASL compiler.
    - optinal [EDK2 Libc](https://github.com/tianocore/edk2-libc): contains a port of libc to a UEFI environment along with UEFI applications that depend on this port of libc.
- [EDK2 platform description (DSC) file spec](https://edk2-docs.gitbook.io/edk-ii-dsc-specification/)
- [UEFI Device Path](https://zhuanlan.zhihu.com/p/351065844)
- [list of known efi protocol guids](https://github.com/biosbits/bits/blob/master/python/efi.py)
- [list of known efi protocol guids](https://github.com/jethrogb/uefireverse/blob/master/guiddb/efi_guid.c)
- [ARM: how to build UEFI firmware on Linux host](https://developer.arm.com/documentation/102571/0100/Build-firmware-on-a-Linux-host)
- [UEFI Events](https://uefi.org/sites/default/files/resources/Understanding%20UEFI%20and%20PI%20Events_Final.pdf)
- [edk2 pkgs dependency](http://vzimmer.blogspot.com/2019/12/10-years-on-and-small-exercise-in.html)

    ```
    $ cd edk2
    $ find . -type f -name "*.inf" -exec egrep -Hn "\.dec" {} \; > 1.dot       # pkg/module.inf: pkg.dec
    $ sed -e "s/^.\/\([^/]*\)\/.*\.inf:.*: \(.*\)\/.*/\1->\2/" 1.dot > 2.dot   # pkg -> pkg
    $ sort 2.dot|uniq > 3.dot
    $ replace self dependency lines
    $ dot -Tsvg 3.dot -o edk2_pkg_dep.svg
    ```

    - similarly, it's possible to generate module-module dependency graph.
- books:
    - "Beyond BIOS Developing with the Unified Extensible Firmware Interface", 3rded, 2017
    - "Harnessing the Uefi Shell Moving the Platform Beyond DOS", 2nd ed, 2017
    - "A Tour Beyond BIOS: Open Source IA Firmware Platform Design Guide in EFI Developer Kit II", v2, 2018
- specs <uefi.org>:
    - uefi spec
    - pi spec
    - acpi spec



Firmware Volume -> Firmware File -> Firmware Section.

FFS (Firmware File System) format:

> The PI Architecture Firmware File System is a binary layout of file storage within firmware
> volumes. It is a flat file system in that there is no provision for any directory hierarchy; all files
> reside in the root directly. Files are stored end to end without any directory entry to describe which
> files are present. Parsing the contents of a firmware volume to obtain a listing of files present
> requires walking the firmware volume from beginning to end.
>
> -- PI spec, vol 3, $2.2.2

Firmware File format:

> The file data of certain file types is sub-divided in a standardized fashion into "Firmware File Sections".
>
> While there are many types of sections, they fall into the following two broad categories:
>
> • Encapsulation sections
> • Leaf sections
>
> Files that are built with sections can be thought of as a tree, with encapsulation sections as nodes and
> leaf sections as the leaves. The file image itself can be thought of as the root and may contain an
> arbitrary number of sections. Sections that exist in the root have no parent section but are still
> considered peers.
>
> --- PI spec, vol 3, $2.1.5

## Background

What is EDK2? Why EDK2 for MyChip? What's needed for enabling EDK2 for MyChip?

### What is EDK2?

>  EDK II is a modern, feature-rich, cross-platform firmware development environment for the UEFI and UEFI Platform Initialization (PI) specifications.
>
> In June of 2004, Intel announced that it would release the “Foundation Code” of its Extensible Firmware Interface (EFI), a successor to the 16-bit x86 “legacy” PC BIOS, under an open source license. This Foundation Code, developed by Intel as part of a project code named Tiano, was Intel’s “preferred implementation” of EFI. This evolved into EDK, EDK II, and other open source projects under the TianoCore community.
>
>The EFI Specifications were contributed to the United EFI Forum as part of the original UEFI Specifications, which has been adopted by over 200 companies and shipped on millions of compute devices. The UEFI Forum does not endorse any particular implementation, but TianoCore is designed to implement the UEFI and UEFI PI specifications.
>
> --- https://www.tianocore.org/

> Tianocore EDK II is the UEFI reference implementation by Intel. EDK is the abbreviation for EFI Development Kit and is developed by the TianoCore community.[1] TianoCore EDK II is the defacto standard generic UEFI services implementation.
>
> --- https://en.wikipedia.org/wiki/TianoCore_EDK_II

So EDK2 is:

- a development environment for UEFI/PI-compatible firmwares;
- a reference UEFI/PI-compatible firmware implementation, evloved from the open source of Intel's `Foundation Code` of EFI (which is part of its `Tiano` project);
- maintained by TianoCore community, and designed to implement the UEFI and UEFI PI specifications;
- not endorsed by UEFI Forum (which does not endorse any particular implementation).

Alternatives ("Most of them do not support standard C style make files, so there will be a learning curve."):

- [GNU-EFI](https://wiki.osdev.org/GNU-EFI) is a very lightweight devloping environment to create UEFI applications.
- close-source vendors:

### Why EDK2?

Questions:

- In what use cases, UEFI-compatible firmware on ARM platform is required? why?
    - ARM aimed to enter general-purpose server market
    - abstraction: need decouple off-the-shelf OSes (particularly Linux) from underlying HW/FW platform: DT is ok for embedded/mobile (where "the vendor controls the kernel"), but not enough for server market (where "The platform/kernel split isn’t a design choice. It is a characteristic of the market").
    - ARM initialtives: SBSA, SBBR, ServerReady/SystemReady, UEFI/ACPI/SMBIOS
- advantages of UEFI/ACPI/SMBIOS-compatible firmware:
    - [UEFI vs BIOS](https://en.wikipedia.org/wiki/Unified_Extensible_Firmware_Interface#Advantages)
    - ACPI vs DT:
        - [Why ACPI on ARM?](http://www.secretlab.ca/archives/151)
        - [ACPI on ARMv8 Servers](https://www.kernel.org/doc/Documentation/arm64/arm-acpi.txt)
        - fdt vs acpi?

            > 对于ARM和PowerPC世界的人来说，FDT（Flattened Device Tree）/DT（Device Tree）已经占据统治地位很久了。它的诞生源于Linus对于ARM各种SOC与Linux kernel driver强耦合性的一次大爆发（说是 pain in the ass）。从此DT的被设计出来了，ARM的耦合性得到了一定的缓解。那时ARM控制着嵌入式和手机世界，X86统治着PC和服务器，曲径分明，井水不犯河水，而ACPI和FDT也相安无事。和平没有持续很久，在X86试图进入手机领域时，ARM也试图进入PC和服务器，大战爆发了。ARM世界的FDT在新战场受到了残酷的抵抗，PC和服务器的玩家们不喜欢FDT，他们希望用一套工具集（toolchain）能同时解决两家问题，他们提出的理由也很有道理：FDT没有ACPI灵活！确实，FDT虽然在提供各种表单方面近似于ACPI，却缺少AML/ASL这样的灵活性。结局是ARM世界宣布在PC和服务器领域全面淘汰FDT，换用ACPI，而在嵌入式系统继续使用FDT。这也是合理的，毕竟嵌入式系统不需要这么多的灵活性，而迁移的代价是巨大的。另一方面，ACPI却随着X86进入嵌入式领域而在X86嵌入式领域生根发芽。
            >
            > --- https://zhuanlan.zhihu.com/p/25893464
    - SMBIOS:
- specific advantages of EDK2 over u-boot?
- does UEFI-firmware stay after OS boot? `UEFI also defines run-time services, for example, time, variable that an OS can invoke at runtime`.
- in terms of security: TEE vs UEFI?
- ARM's commitment on EDK2:

    > The EDKII project is an open source project that provides a modern, feature-rich, cross-platform firmware development environment for the UEFI and PI specifications developed and maintained by the UEFI Forum.
    >
    > Arm contributions make sure the EDKII project constantly keeps an up to date implementation of a UEFI compliant firmware on Arm systems.
    >
    > Arm contributes to both the EDKII main repository, maintaining some core packages like DynamicTablesPkg and StandaloneMMPkg, and the EDKII platforms repository, hosting support for various Arm reference platforms as well as other 3rd party Arm-based platforms maintained by either Linaro or partners.
    > --- https://developer.arm.com/tools-and-software/open-source-software/firmware/edkii-uefi-firmware


### MyChip: what's needed to be done in firmware

For MyChip to support EDK2 (or pass ARM's ServerReady test ACS), the following is to be done:

- Firmware
    - ATF:
    - EDK2:
- Linux
    - Drivers:
    - Kernel:





## Linux Boot process (`r5.14`)

below are To Be Confirmed...

- kernel config:
    - `CONFIG_EFI_STUB`: EFI_STUB support, 即会在kernel前面加PE/COFF头
    - `CONFIG_EFI`: EFI runtime service support
    - `CONFIG_EFI_ARMSTUB_DTB_LOADER`: 是否让 EFI_STUB 读取通过 cmdline 指定的 `dtb=`.
- 对于有PE/COFF头的kernel image:
    - 仅当直接在 UEFI Shell 中执行 vmlinux (带`PE/COFF`头) 时, 才会执行`EFI_STUB`, 入口为 `efi-stub.c:efi_pe_entry()`.
    - 如何确定`EFI_STUB`的入口为`efi-stub.c:efi_pe_entry()`呢？
         - https://s-matyukevich.github.io/raspberry-pi-os/docs/lesson01/linux/kernel-startup.html
         - https://docs.kernel.org/admin-guide/efi-stub.html
         - `.head.text` in link script: https://elixir.bootlin.com/linux/v5.14.17/source/arch/arm64/kernel/vmlinux.lds.S
         - `AddressOfEntryPoint: __efistub_efi_pe_entry - .L_head`: https://elixir.bootlin.com/linux/v5.14.17/source/arch/arm64/kernel/efi-header.S#L49
         - `OBJCOPYFLAGS := --prefix-symbols=__efistub_`: `__efistub_efi_pe_entry()` => `efi_pe_entry()`
    - 当用`u-boot`或`grub`作为bootloader时,  `EFI_STUB` 实际并不起作用: 从第一条指令开始执行: 第一条指令为 nop, 第二条指令跳转到 `primary_entry`.
         - `u-boot` 在使用`fit` image (即`.itb`文件, 由`mkimage`工具读取对应的`.its`配置文件生成)启动时, 一般情况下,               会根据itb中的config选择kernel/ramdisk/fdt这三个image:
             - 对于 fit中 type 为 kernel 的 image, u-boot会遵循其指定的 load address 和 entry point。
             - 对于 ramdisk/fdt, u-boot会自行alloc内存去load它们.
             - `u-boot`的`bootm [addr [arg ...]]`命令可以带三个参数，第一个是kernel             入口地址，第二个是initrd地址(若没有, 则可用`-`占位)，第三个是fdt地址.
- `EFI STUB`的功能在于: setup environment according to [ARM64 boot protocol](https://github.com/torvalds/linux/blob/master/Documentation/arm64/booting.rst), then jump to kernel entry `primary_entry()`, where `primary` means "the primary cpu". Wrt DTB, basically it prepares a DTB and update the DTB with the following info into the `chosen` node:
    - EFI system table related
    - bootargs(cmdline)
    - initrd addr/size
    - [reserved mem](https://www.kernel.org/doc/Documentation/devicetree/bindings/reserved-memory/reserved-memory.txt)
- 在 uefi config table 中包含 fdt: 通过`drivers/firmware/efi/libstub/fdt.c:get_fdt()`获取

So it seems that the only "parameter" (`x0`) passed to kernel is the addr of fdt, which in tern contains all the rest info required by kernel.

```
efi_pe_entry(handle, sys_table)               <= drivers/firmware/efi/libstub/efi-stub.c
|-- check EFI_SYSTEM_TABLE_SIGNATURE
|-- check_platform_features()
|-- efi_convert_cmdline()                      <= from utf-16 to ascii
|-- efi_parse_options()
|-- efi_info("Booting Linux Kernel...\n");     <= "Booting Linux Kernel..."
|-- setup_graphics()
|-- handle_kernel_image()                      <= relocate kernel if needed
|-- efi_retrieve_tpm2_enventlog()
|-- efi_enable_reset_attack_mitigation()
|-- efi_get_secureboot()
|-- handle dtb
|   |-- if (CONFIG_EFI_ARMSTUB_DTB_LOADER && efi_secureboot_mode_disabled)
|   |   |-- efi_load_dtb()
|   |   |   `-- handle_cmdline_files(image, L"dtb="...)
|   |   `-- efi_info("Using DTB from command line\n");
|   |-- else
|   |   |-- efi_err("Ignoring DTB from command line.\n");
|   |    `-- get_fdt()                          <= get FDT from sys config table
|   `-- if (!fdt_addr) efi_info("Generating empty DTB\n");
|-- efi_load_initrd()
|-- efi_random_get_seed()
|-- get_efi_config_table()
|-- install_memreserve_table()
|-- allocate_new_fdt_and_exit_boot()           <= allocate new FDT and add EFI/bootargs/initrd fields to the FDT
|   `-- update_fdt()                           <= drivers/firmware/efi/libstub/fdt.c
|       |-- ...
|       |-- fdt_del_mem_rsv()                  <= delete all memory reserve map entries. When booting via UEFI,
|       `--...                                    kernel will use the UEFI memory map to find reserved regions.
`-- efi_enter_kernel(image_addr, fdt_addr, fdt_size);  <= arch/arm64/kernel/efi-entry.S
    |-- dcache_clean_poc()
    |-- ic ialluis
    |-- turn off dcache and mmu
    |-- x0=fdt_addr
    `-- br x19                                   <= x19: primary_entry
```

Kernel entry point:

```
b primary_entry                    <= arch/arm64/kernel/head.S
|-- preserve_boot_args()
|   |-- x21=x0                     <= x21=FDT
|   |-- bootargs[0:3]=x0~x3
|   `-- dcache_inval_poc
|-- init_kernel_el()
|-- setup_cpu_boot_mode_flag()
|-- __create_page_tables()
|-- __cpu_setup()
`-- __primary_switch()
    |-- __enable_mmu()
    |-- __relocate_kernel()
    |-- adrp x0, __PHYS_OFFSET    <= __PHYS_OFFSET=KERNEL_START=_text
    `-- __primary_switched()
        |-- init_cpu_task
        |-- __fdt_pointer=x21     <= save FDT pointer
        |-- __pi_memset()         <= clear bss
        |-- kasan_early_init()
        |-- mov x0, x21           <= pass FDT address in x0
        |-- early_fdt_map()
        |-- init_feature_override()
        |-- switch_to_vhe()
        `-- start_kernel()        <= init/main.c
	          |-- set_task_stack_end_magic(&init_task)
	          |-- smp_setup_processor_id()
              |   `-- pr_info("Booting Linux on physical CPU ...",...)
	          |-- debug_objects_early_init()
	          |-- init_vmlinux_build_id()
              |-- cgroup_init_early()
              |-- local_irq_disable()
	          |-- boot_cpu_init()
              |-- page_address_init()
              |-- pr_notice("%s", linux_banner)     <== "Linux version ..."
              |-- early_security_init()
              |-- setup_arch(&command_line)
              |   |-- setup_initial_init_mm()
              |   |-- ...
              |   |-- setup_machine_fdt()
              |   |   |-- ...
              |   |   `-- pr_info("Machine model...", ...) <= "Machine model: ..."
              |   |-- ...
              |   |-- efi_init()
              |   |   |-- sys_tbl= efi_get_fdt_params()     <= grab UEFI info placed in fdt by stub
              |   |   |   |-- ...
              |   |   |   `-- pr_info("UEFI not found.\n")  <== if no UEFI info found
              |   |   |-- efi_memmap_init_early()           <== If we are booting via UEFI, the UEFI mem map
              |   |   |                                         is the only description of mem we have.
              |   |   |-- uefi_init(sys_tbl)
              |   |   `-- ...
              |   `-- ...
              |-- setup_boot_config()
              |-- setup_command_line(command_line)
              |-- setup_nr_cpu_ids()
              |-- setup_per_cpu_areas()
              |-- smp_prepare_boot_cpu()
              |-- boot_cpu_hotplug_init()
              |-- build_all_zonelists(NULL)
              |-- page_alloc_init()
              |-- pr_notice("Kernel command line:...",...) <= "Kernel command line: "
              `-- ...
```

## EDk2 for Pi4B

### Build `RPI_EFI.fd`

Following [official instruction](https://github.com/tianocore/edk2-platforms#how-to-build-linux-environment):

Suppose that the cross-compiling toolchain (`gcc-arm-10.2-2020.11-x86_64-aarch64-none-linux-gnu`) is already installed. The following command install utilities needed during the build process:

```
$ sudo apt install uuid-dev acpica-tools nasm  # uuidgen, iasl
```

Now pull the repositories:

```
$ mkdir ~/work/tianocore
$ cd tianocore
$ git clone https://github.com/tianocore/edk2.git
$ git submodule update --init
$ git clone https://github.com/tianocore/edk2-platforms.git
$ git submodule update --init
$ git clone https://github.com/tianocore/edk2-non-osi.git
$ git clone https://github.com/tianocore/edk2-libc.git
```

Use the following script to build the `BasicTools`:

```
export WORKSPACE=/home/bruin/work/tianocore
export PACKAGES_PATH=$WORKSPACE/edk2:$WORKSPACE/edk2-platforms:$WORKSPACE/edk2-non-osi
pushd $WORKSPACE
source edk2/edksetup.sh
echo "Building BaseTools..."
make -C edk2/BaseTools $1
popd
```

The following `BasicTools` are generated under  `edk2/BaseTools/Source/C/bin/` (go `edk2/BaseTools/UserManuals/` for their description):

- BrotliCompress
- DevicePath
- EfiRom
- GenCrc32
- GenFfs
- GenFv
- GenFw
- GenSec
- LzmaCompress
- TianoCompress
- VfrCompile
- VolInfo

There is also a python script `build` under ` edk2/BaseTools/BinWrappers/PosixLike/`, which drives the rest of the build process.

Use the following script to build UEFI firmware:

```
export WORKSPACE=/home/bruin/work/tianocore
export PACKAGES_PATH=$WORKSPACE/edk2:$WORKSPACE/edk2-platforms:$WORKSPACE/edk2-non-osi
pushd $WORKSPACE
source edk2/edksetup.sh
echo "Building firmware for Pi4B..."
GCC5_AARCH64_PREFIX=aarch64-none-linux-gnu- build \
      -n 4 \
      -a AARCH64 \
      -p Platform/RaspberryPi/RPi4/RPi4.dsc \
      -t GCC5 \
      -b DEBUG \
      all
popd
```

The build results are stored under `tianocore/Build/RPi4/DEBUG_GCC5/`. Particularly, the final flash device binary image `RPI_EFI.fd` is located under `tianocore/Build/RPi4/DEBUG_GCC5/FV/`.



### Use of `RPI_EFI.fd`

Booting into `UEFI Shell`, which is one of "boot device".

Instruction:

- `edk2-platforms/Platform/RaspberryPi/RPi4/Readme.md`
- `readme.md` inside `https://github.com/pftf/RPi4/releases/download/v1.17/RPi4_UEFI_Firmware_v1.32.zip`
- [rpi-update](https://github.com/raspberrypi/rpi-update): `sudo JUST_CHECK=1 rpi-update` (pi需要能够连到github.com)
- [Q&A for using `RPI_EFI.fd`](https://github.com/pftf/RPi4/issues/189)

- pi4b firmware manual download: https://github.com/raspberrypi/firmware/tree/master/boot
    - `fixup4.dat`
    - `start4.elf`


#### v1.17

注: 下面各种场景下出错的原因在于`start4.elf`和`fixup4.dat`没有使用最新的版本。

所谓 v1.17的方式，是指按照 <https://github.com/pftf/RPi4/releases/tag/v1.17> 版本的 readme 来使用 `RPI_EFI.fd`.

首先试 net boot 环境。

在 `boot/config.txt` 中加:

```
#####################################
# EDK2
#####################################
enable_gic=1
disable_commandline_tags=2
device_tree_address=0x1f0000
device_tree_end=0x200000
armstub=RPI_EFI.fd
kernel_address=0x400000
```

最后一行 `kernel_address=0x400000` 是为了不让 `kernel8.img` 冲掉 `RPI_EFI.fd`, 不然启动过程中报错:

```
MESS:00:00:19.120628:0: brfs: File read: /mfs/sd/RPI_EFI.fd
MESS:00:00:19.123089:0: Loading 'RPI_EFI.fd' to 0x0 size 0x1f0000
MESS:00:00:19.128919:0: brfs: File read: 2031616 bytes
MESS:00:00:21.033784:0: brfs: File read: /mfs/sd/kernel8.img
MESS:00:00:21.036341:0: Loading 'kernel8.img' to 0x80000 size 0x789b6a
MESS:00:00:22.176546:0: Kernel relocated to 0x200000
MESS:00:00:22.178401:0: Device tree loaded to 0x1f0000 (size 0xc7ca)
MESS:00:00:22.186018:0: uart: Set PL011 baud rate to 103448.300000 Hz
MESS:00:00:22.193553:0: uart: Baud rate change done...
MESS:00:00:22.195575:0: uart: Baud rate change done...
MESS:00:00:22.212101:0: genet: GENET STOP: 0
NOTICE:  BL31: v2.5(release):
NOTICE:  BL31: Built : 18:50:30, Jun 14 2021
UEFI firmware (version EDK2-DEV built at 15:25:09 on Oct 20 2021)
Board Rev: 0xB03114
RAM < 1GB: 0x00000000 (Size 0x3B400000)
VideoCore: 0x3B400000 (Size 0x04C00000)
Total RAM: 0x80000000
FD:
        PhysicalBase: 0x0
        VirtualBase: 0x0
        Length: 0x1D0000
FD Variables:
        PhysicalBase: 0x1D0000
        VirtualBase: 0x1D0000
        Length: 0x20000
Flattened Device Tree:
        PhysicalBase: 0x1F0000
        VirtualBase: 0x1F0000
        Length: 0x10000
System RAM < 1GB:
        PhysicalBase: 0x200000
        VirtualBase: 0x200000
        Length: 0x3B200000
GPU Reserved:
        PhysicalBase: 0x3B400000
        VirtualBase: 0x3B400000
        Length: 0x4C00000
SoC Reserved (27xx):
        PhysicalBase: 0xFC000000
        VirtualBase: 0xFC000000
        Length: 0x2000000
SoC Reserved (283x):
        PhysicalBase: 0xFE000000
        VirtualBase: 0xFE000000
        Length: 0x2000000
Extended System RAM < 3GB:
        PhysicalBase: 0x40000000
        VirtualBase: 0x40000000
        Length: 0x40000000
Decompress Failed - Invalid Parameter

ASSERT_EFI_ERROR (Status = Not Found)
ASSERT [ArmPlatformPrePiUniCore] /home/bruin/work/tianocore/edk2/ArmPlatformPkg/PrePi/PrePi.c(152): !EFI_ERROR (Status)
```

在"正常"情况下, boot分区没有kernel的image, 所以不会 load kernel:

```
...
MESS:00:00:51.799999:0: Loading 'RPI_EFI.fd' to 0x0 size 0x1f0000
MESS:00:00:51.805825:0: No compatible kernel found
MESS:00:00:51.810327:0: Device tree loaded to 0x1f0000 (size 0xc85a)
...
```

另外，从log中可以推断，前 2M RAM空间的 layout 如下 (其中FD的最前面是`BL31.bin`):

```
|<--- RPI_EFI.fd ---->|
+-------------+-------+----+
| FD          |  FD   |dev |
|             |  vars |tree|
+-------------+-------+----+
   1856K        128K   64K
```

另外，前 1G RAM 空间中尾部 76M 分配给了 GPU, 4G尾部64M分配给了外设, 阴影部分为空:

```
                  1G                2G                3G                4G
+-------------+---+-----------------+-----------------+------------+----+
|    ARM      |GPU|     ARM         |/////////////////|////////////|peri|
+-------------+---+-----------------+-----------------+------------+----+
               76M                                                  64M
```


加了 `kernel_address=0x400000` 以后, 出错在SD相关(此时 pi 中没有插sd卡):

```
...
Extended System RAM < 3GB:
        PhysicalBase: 0x40000000
        VirtualBase: 0x40000000
        Length: 0x40000000
add-symbol-file /home/bruin/work/tianocore/Build/RPi4/DEBUG_GCC5/AARCH64/MdeModulePkg/Core/Dxe/DxeMain/DEBUG/DxeCore.dll 0x3A553000
Loading DxeCore at 0x003A552000 EntryPoint=0x003A55A2F0
CoreInitializeMemoryServices:
  BaseAddress - 0x200000 Length - 0x37200000 MinimalMemorySizeNeeded - 0x34AE000
InstallProtocolInterface: 5B1B31A1-9562-11D2-8E3F-00A0C969723B 3A57B7D0
ProtectUefiImageCommon - 0x3A57B7D0
  - 0x000000003A552000 - 0x0000000000047000
InstallProtocolInterface: C85D06BE-5F75-48CE-A80F-1236BA3B87B1 3A57BFD0
DxeMain: MemoryBaseAddress=0x200000 MemoryLength=0x37200000
add-symbol-file /home/bruin/work/tianocore/Build/RPi4/DEBUG_GCC5/AARCH64/MdeModulePkg/Core/Dxe/DxeMain/DEBUG/DxeCore.dll 0x3A553000
HOBLIST address in DXE = 0x36E36018
Memory Allocation 0x00000004 0x3B3F8000 - 0x3B3F8FFF
Memory Allocation 0x00000000 0x0 - 0x1CFFFF
Memory Allocation 0x00000006 0x1D0000 - 0x1EFFFF
Memory Allocation 0x00000000 0x1F0000 - 0x1FFFFF
Memory Allocation 0x00000004 0x3B3F7000 - 0x3B3F7FFF
Memory Allocation 0x00000004 0x3B3F6000 - 0x3B3F6FFF
Memory Allocation 0x00000004 0x3B3F5000 - 0x3B3F5FFF
Memory Allocation 0x00000004 0x3B3F4000 - 0x3B3F4FFF
Memory Allocation 0x00000004 0x3B3F3000 - 0x3B3F3FFF
Memory Allocation 0x00000004 0x3B3F9000 - 0x3B3FFFFF
Memory Allocation 0x00000004 0x3B3E3000 - 0x3B3F2FFF
Memory Allocation 0x00000004 0x3ACBE000 - 0x3B3E2FFF
Memory Allocation 0x00000004 0x3A599000 - 0x3ACBDFFF
Memory Allocation 0x00000003 0x3A552000 - 0x3A598FFF
Memory Allocation 0x00000003 0x3A552000 - 0x3A598FFF
FV Hob            0x20000 - 0x1CFFFF
FV Hob            0x3A599000 - 0x3ACBC27F
FV2 Hob           0x3A599000 - 0x3ACBC27F
                  9A15AA37-D555-4A4E-B541-86391FF68164 - 9E21FD93-9C72-4C15-8C4B-E77F1DB2D792
InstallProtocolInterface: D8117CFE-94A6-11D4-9A3A-0090273FC14D 3A57B0B0
...
SD is routed to emmc2
InstallProtocolInterface: 3E591C00-9E4A-11DF-9244-0002A5F5F51B 36E3E028
InstallProtocolInterface: 964E5B21-6459-11D2-8E39-00A0C969723B 3607BA48
InstallProtocolInterface: 09576E91-6D3F-11D2-8E39-00A0C969723B 3607B518
RpiFirmwareGetClockRate: Get Clock Rate return: ClockRate=0 ClockId=C
ASSERT [ArasanMMCHost] /home/bruin/work/tianocore/edk2-platforms/Platform/RaspberryPi/
Drivers/ArasanMmcHostDxe/ArasanMmcHostDxe.c(263): BaseFrequency != 0
```

在不插SD卡的情况下，通过USB启动，也是报同样的错误。在换了SD卡启动以后，仍然报同样的错误:

```
RpiFirmwareGetClockRate: Get Clock Rate return: ClockRate=0 ClockId=C
ASSERT [ArasanMMCHost] /home/bruin/work/tianocore/edk2-platforms/Platform/RaspberryPi/
Drivers/ArasanMmcHostDxe/ArasanMmcHostDxe.c(263): BaseFrequency != 0
```


换成 <https://github.com/pftf/RPi4/releases/tag/v1.17> 的文件, 接上显示器，启动到UEFI以后是一片空白。

#### v1.32

用 <https://github.com/pftf/RPi4/releases/tag/v1.32> 带的 `start4.elf`/`fixup4.dat` 加上本地编译的 `RPI_EFI.fd`, 可以成功进入 UEFI shell. 启动后串口的输出(按回车进入菜单界面, 从`Boot Manager`菜单项可以选择作为启动选项之一的 `UEFI Shell` ):

```
...
MESS:00:00:51.810278:0: Loading 'RPI_EFI.fd' to 0x0 size 0x1f0000
MESS:00:00:51.816103:0: No compatible kernel found
MESS:00:00:51.820605:0: Device tree loaded to 0x1f0000 (size 0xc908)
MESS:00:00:51.828256:0: uart: Set PL011 baud rate to 103448.300000 Hz
MESS:00:00:51.835760:0: uart: Baud rate change done...
MESS:00:00:51.837780:0: uart: Baud rate change done...
MESS:00:00:51.842926:0: bfs_xhci_stop
MESS:00:00:51.846026:0: XHCI-STOP
MESS:00:00:51.849144:0: xHC ver: 256 HCS: 05000420 fc000031 00e70004 HCC: 002841eb
MESS:00:00:51.856368:0: USBSTS 18
NOTICE:  BL31: v2.5(release):
NOTICE:  BL31: Built : 18:50:30, Jun 14 2021
UEFI firmware (version UEFI Firmware v1.32 built at 19:05:58 on Oct 19 2021)


ESC (setup), F1 (shell), ENTER (boot)......
  Error: Could not detect network connection.
  Error: Could not detect network connection.
BdsDxe: No bootable option or device was found.
BdsDxe: Press any key to enter the Boot Manager Menu.


Raspberry Pi 4 Model B
 BCM2711 (ARM Cortex-A72)                            1.50 GHz
 UEFI Firmware v1.32                                 2048 MB RAM

   Select Language            <English>                  This is the option
                                                         one adjusts to change
 > Device Manager                                        the language for the
 > Boot Manager                                          current system
 > Boot Maintenance Manager

   Continue
   Reset

  ^v=Move Highlight       <Enter>=Select Entry
```

进入 Shell 以后:


```
InstallProtocolInterface: 387477C2-69C7-11D2-8E39-00A0C969723B 35876020
InstallProtocolInterface: 752F3136-4E16-4FDC-A22A-E5F46812F4CA 35876A98
InstallProtocolInterface: 6302D008-7F9B-4F30-87AC-60C9FEF5DA4E 3389B9F0
UEFI Interactive Shell v2.2
EDK II
UEFI v2.70 (EDK2, 0x00010000)
Mapping table
      FS0: Alias(s):HD0a0a0b:;BLK1:
          PcieRoot(0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/USB(0x0,0x0)/USB(0x0,0x0)/HD(1
,MBR,0x04EA7D7A,0x800,0x100000)
     BLK2: Alias(s):
          VenHw(100C2CFA-B586-4198-9B4C-1683D195B1DA)
     BLK0: Alias(s):
          PcieRoot(0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/USB(0x0,0x0)/USB(0x0,0x0)
Press ESC in 1 seconds to skip startup.nsh or any other key to continue.
Shell> fs0:
FSOpen: Open '\' Success
FS0:\> ls
FSOpen: Open '.' Success
FSOpen: Open '\System Volume Information' Success
FSOpen: Open '\overlays' Success
FSOpen: Open '\bcm2711-rpi-4-b.dtb' Success
FSOpen: Open '\config.txt' Success
FSOpen: Open '\fixup4.dat' Success
FSOpen: Open '\Readme.md' Success
FSOpen: Open '\start4.elf' Success
FSOpen: Open '\RPI_EFI.fd' Success
Directory of: FS0:\
10/19/2021  19:06              49,829  bcm2711-rpi-4-b.dtb
10/19/2021  18:57                 206  config.txt
10/19/2021  19:06               5,351  fixup4.dat
10/19/2021  19:06 <DIR>         4,096  overlays
10/19/2021  18:57               5,067  Readme.md
10/19/2021  19:20           2,031,616  RPI_EFI.fd
10/19/2021  19:06           2,243,232  start4.elf
          8 File(s)   6,366,959 bytes
          1 Dir(s)
FSOpen: Open '\' Success
FS0:\> memmap
Type       Start            End              # Pages          Attributes
Reserved   0000000000000000-00000000001CFFFF 00000000000001D0 000000000000000E
RT_Data    00000000001D0000-00000000001EFFFF 0000000000000020 800000000000000E
Reserved   00000000001F0000-00000000001FFFFF 0000000000000010 000000000000000E
Available  0000000000200000-000000003368FFFF 0000000000033490 000000000000000E
RT_Data    0000000033690000-000000003374FFFF 00000000000000C0 800000000000000E
Available  0000000033750000-00000000337B3FFF 0000000000000064 000000000000000E
LoaderCode 00000000337B4000-00000000338AFFFF 00000000000000FC 000000000000000E
RT_Data    00000000338B0000-00000000338BFFFF 0000000000000010 800000000000000E
Available  00000000338C0000-00000000338F1FFF 0000000000000032 000000000000000E
Reserved   00000000338F2000-0000000033BDFFFF 00000000000002EE 000000000000000E
Available  0000000033BE0000-0000000033C0DFFF 000000000000002E 000000000000000E
LoaderCode 0000000033C0E000-0000000033C37FFF 000000000000002A 000000000000000E
BS_Code    0000000033C38000-0000000033C7FFFF 0000000000000048 000000000000000E
RT_Data    0000000033C80000-0000000033CAFFFF 0000000000000030 800000000000000E
RT_Code    0000000033CB0000-0000000033D6FFFF 00000000000000C0 800000000000000E
ACPI_Recl  0000000033D70000-0000000033D7FFFF 0000000000000010 000000000000000E
RT_Data    0000000033D80000-0000000033D9FFFF 0000000000000020 800000000000000E
RT_Code    0000000033DA0000-0000000033E3FFFF 00000000000000A0 800000000000000E
Available  0000000033E40000-000000003563DFFF 00000000000017FE 000000000000000E
BS_Data    000000003563E000-000000003565BFFF 000000000000001E 000000000000000E
Available  000000003565C000-0000000035679FFF 000000000000001E 000000000000000E
BS_Data    000000003567A000-00000000356C1FFF 0000000000000048 000000000000000E
Available  00000000356C2000-00000000356C5FFF 0000000000000004 000000000000000E
BS_Data    00000000356C6000-00000000356D2FFF 000000000000000D 000000000000000E
Available  00000000356D3000-00000000356DAFFF 0000000000000008 000000000000000E
BS_Data    00000000356DB000-00000000357FDFFF 0000000000000123 000000000000000E
Available  00000000357FE000-0000000035800FFF 0000000000000003 000000000000000E
BS_Data    0000000035801000-0000000035805FFF 0000000000000005 000000000000000E
Available  0000000035806000-0000000035806FFF 0000000000000001 000000000000000E
BS_Data    0000000035807000-0000000035812FFF 000000000000000C 000000000000000E
Available  0000000035813000-0000000035813FFF 0000000000000001 000000000000000E
BS_Data    0000000035814000-0000000036D37FFF 0000000000001524 000000000000000E
BS_Code    0000000036D38000-000000003711FFFF 00000000000003E8 000000000000000E
RT_Code    0000000037120000-00000000371AFFFF 0000000000000090 800000000000000E
Available  00000000371B0000-00000000371BFFFF 0000000000000010 000000000000000E
RT_Data    00000000371C0000-00000000372DFFFF 0000000000000120 800000000000000E
Available  00000000372E0000-00000000372FEFFF 000000000000001F 000000000000000E
BS_Data    00000000372FF000-00000000372FFFFF 0000000000000001 000000000000000E
Available  0000000037300000-000000003A44FFFF 0000000000003150 000000000000000E
BS_Code    000000003A450000-000000003A496FFF 0000000000000047 000000000000000E
BS_Data    000000003A497000-000000003B2FFFFF 0000000000000E69 000000000000000E
Available  0000000040000000-000000007FFFFFFF 0000000000040000 000000000000000E

  Reserved  :          1,230 Pages (5,038,080 Bytes)
  LoaderCode:            294 Pages (1,204,224 Bytes)
  LoaderData:              0 Pages (0 Bytes)
  BS_Code   :          1,143 Pages (4,681,728 Bytes)
  BS_Data   :          9,525 Pages (39,014,400 Bytes)
  RT_Code   :            496 Pages (2,031,616 Bytes)
  RT_Data   :            608 Pages (2,490,368 Bytes)
  ACPI_Recl :             16 Pages (65,536 Bytes)
  ACPI_NVS  :              0 Pages (0 Bytes)
  MMIO      :              0 Pages (0 Bytes)
  MMIO_Port :              0 Pages (0 Bytes)
  PalCode   :              0 Pages (0 Bytes)
  Available :        491,264 Pages (2,012,217,344 Bytes)
  Persistent:              0 Pages (0 Bytes)
              --------------
Total Memory:          1,966 MB (2,061,705,216 Bytes)
```


- [how to enter the UEFI shell of a computer](https://superuser.com/a/1057594/944487)

### Anatomy of `RPI_EFI.fd`

ref:

- http://william30101.blogspot.com/2012/06/uefi-framework-7-volume-files-and.html
- https://github.com/theopolis/uefi-firmware-parser
- https://github.com/LongSoft/UEFITool
- [AMI's mmtool](https://www.ami.com/what-is-mmtool/): [how to use mmtool](https://winraid.level1techs.com/t/howto-get-full-nvme-support-for-all-systems-with-an-ami-uefi-bios/30901#msg14810)
- [UBU: UEFI BIOS Updater](https://winraid.level1techs.com/t/tool-guide-news-uefi-bios-updater-ubu/30357)
- `$ sudo apt install uefitool uefitool-cli && UEFITool`
- https://sudonull.com/post/125061-UEFI-BIOS-file-device-part-two-UEFI-Firmware-Volume-and-its-contents
- VolInfo: ./edk2/BaseTools/Source/C/bin/VolInfo

Hierarchy:

- FD: Flash Device
- FV: Firmware Volumes, 相当于一个逻辑卷(分区)，其上创建 FFS 文件系统
- FF: Firmware Files
- Firmware Sections (注: section 类型还可以是 Volume image, compressed).

`RPI_EFI.fd` 的前128K为 `./edk2-non-osi/Platform/RaspberryPi/RPi4/TrustedFirmware/bl31.bin` (padded with `0xff`).

```
bruin@u2004 ~/work/tianocore/Build/RPi4/DEBUG_GCC5/FV $ diff bl31.bin.xxd 128K.bin.xxd
2567c2567,8192
< 0000a060: 0100 0000 1400 0000 0104 01              ...........
---
> 0000a060: 0100 0000 1400 0000 0104 01ff ffff ffff  ................
...
> 0001ffe0: ffff ffff ffff ffff ffff ffff ffff ffff  ................
> 0001fff0: ffff ffff ffff ffff ffff ffff ffff ffff  ................
```

从128K开始，是 Flash Volumn. 这个 FV 为 FFSv2 文件系统， 包括两个文件，第二个文件是一个压缩的 FV 镜像，即编译过程中生成的`FVMAIN.Fv`(~7M), 压缩为`FVMAIN_COMPACT.Fv`(~1.7M).

> UEFI and PI specifications define the standardized format for EFI firmware storage devices (FLASH or other non-volatile storage) which are abstracted into "Firmware Volumes".
> ...
> A Firmware Volume (FV) is a file level interface to firmware storage. Multiple FVs may be present in a single FLASH device, or a single FV may span multiple FLASH devices. An FV may be produced to support some other type of storage entirely, such as a disk partition or network device. In all cases, an FV is formatted with a binary file system. The file system used is typically the Firmware File System (FFS), but other file systems may be possible in some cases. Hence, all modules are stored as "files" in the FV.
>
> Files themselves have an internally defined binary format. This format allows for implementation of security, compression, signing, etc. Within this format, there are one or more "leaf" images. A leaf image could be, for example, a PE32 image for a DXE driver.
>
> Therefore, there are several layers of organization to a full UEFI/PI firmware image. These layers are illustrated below in Figure 1. Each transition between layers implies a processing step that transforms or combines previously processed files into the next higher level. Also shown in Figure 1 are the reference implementation tools that process the files to move them between the different layers.
>
>
> ```{r echo=FALSE, out.width='80%', fig.align='center', fig.pos = 'h', fig.cap="Fig 1: Firmware Image hierarchy"}
> knitr::include_graphics("./images/firmware-image-layers.png")
> ```

> --- https://edk2-docs.gitbook.io/edk-ii-build-specification/2_design_discussion/22_uefipi_firmware_images

```
$ sudo pip install uefi_firmware
$ /usr/local/bin/uefi-firmware-parser --brute ~/work/tianocore/Build/RPi4/DEBUG_GCC5/FV/RPI_EFI.fd
Found volume magic at 0x20000            <== 前 128K 可视为padding, 最前面是 bl31.bin
Firmware Volume: 8c8ce578-8a3d-4f1c-9935-896185c32dd3 attr 0x000cfeff, rev 2, cksum 0xb4b8, size 0x1b0000 (1769472 bytes)
  Firmware Volume Blocks: (432, 0x1000)  <== 共432个block, 每个block 4K. 故 volumn size=0x1b0000.
  File 0: 3e401783-cc94-4fcd-97bc-bd35ac369d2f type 0x03, attr 0x04, state 0x07, size 0x9578 (38264 bytes), (security core)
    Section 0: type 0x18, size 0xfc (252 bytes) (Free-form GUID section)
    Section 1: type 0x12, size 0x9464 (37988 bytes) (Terse executable (TE) section)
  File 1: 9e21fd93-9c72-4c15-8c4b-e77f1db2d792 type 0x0b, attr 0x00, state 0x07, size 0x13c8fc (1296636 bytes), (firmware volume image)
    Section 0: type 0x02, size 0x13c8e4 (1296612 bytes) (Guid Defined section)  <== 压缩格式 LZMA
      Guid-Defined: ee4e5898-3914-4259-9d6e-dc7bd79403cf offset= 0x18 attrs= 0x1 (PROCESSING_REQUIRED)
        Section 0: type 0x19, size 0xc (12 bytes) (Raw section)
        Section 1: type 0x17, size 0x723284 (7484036 bytes) (Firmware volume image section)
          Firmware Volume: 8c8ce578-8a3d-4f1c-9935-896185c32dd3 attr 0x0004feff, rev 2, cksum 0xfa72, size 0x723280 (7484032 bytes)
            Firmware Volume Blocks: (116938, 0x40) <== 共116938个block, 每个 block 0x40 字节。共0x723280字节。
            File 0: ffffffff-ffff-ffff-ffff-ffffffffffff type 0xf0, attr 0x00, state 0x07, size 0x2c (44 bytes), (ffs padding)
            File 1: d6a2cb7f-6a18-4e2f-b43b-9920a733700a type 0x05, attr 0x00, state 0x07, size 0x47030 (290864 bytes), (dxe core)
              Section 0: type 0x10, size 0x47004 (290820 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x14 (20 bytes) (User interface name section)
              Name: DxeCore
            File 2: 80cf7257-87ab-47f9-a3fe-d50b76d89541 type 0x07, attr 0x00, state 0x07, size 0x96da (38618 bytes), (driver)
              Section 0: type 0x19, size 0x6a4 (1700 bytes) (Raw section)
              Section 1: type 0x13, size 0x6 (6 bytes) (DXE dependency expression section)
                TRUE
                END
              Section 2: type 0x10, size 0x9004 (36868 bytes) (PE32 image section)
              Section 3: type 0x15, size 0x12 (18 bytes) (User interface name section)
              Name: PcdDxe
            File 3: b8d9777e-d72a-451f-9bdb-bafb52a68415 type 0x07, attr 0x00, state 0x07, size 0xc070 (49264 bytes), (driver)
              Section 0: type 0x13, size 0x3a (58 bytes) (DXE dependency expression section)
                PUSH 2890b3ea-053d-1643-ad0c-d64808da3ff1
                PUSH 32898322-2da1-474a-baaa-f3f7cf569470
                OR
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                AND
                END
              Section 1: type 0x10, size 0xc004 (49156 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x18 (24 bytes) (User interface name section)
              Name: ArmCpuDxe
            File 4: b601f8c4-43b7-4784-95b1-f4226cb40cee type 0x07, attr 0x00, state 0x07, size 0x4004e (262222 bytes), (driver)
              Section 0: type 0x13, size 0x16 (22 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                END
              Section 1: type 0x10, size 0x40004 (262148 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x1a (26 bytes) (User interface name section)
              Name: RuntimeDxe
            File 5: f80697e9-7fd6-4665-8646-88e33ef71dfc type 0x07, attr 0x00, state 0x07, size 0xa058 (41048 bytes), (driver)
              Section 0: type 0x13, size 0x16 (22 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                END
              Section 1: type 0x10, size 0xa004 (40964 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x24 (36 bytes) (User interface name section)
              Name: SecurityStubDxe
            File 6: 42857f0a-13f2-4b21-8a23-53d3f714b840 type 0x07, attr 0x00, state 0x07, size 0x3006c (196716 bytes), (driver)
              Section 0: type 0x13, size 0x28 (40 bytes) (DXE dependency expression section)
                PUSH 6441f818-6362-4e44-b570-7dba31dd2453
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                AND
                END
              Section 1: type 0x10, size 0x30004 (196612 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x28 (40 bytes) (User interface name section)
              Name: CapsuleRuntimeDxe
            File 7: 733cbac2-b23f-4b92-bc8e-fb01ce5907b7 type 0x07, attr 0x00, state 0x07, size 0x4005e (262238 bytes), (driver)
              Section 0: type 0x13, size 0x16 (22 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                END
              Section 1: type 0x10, size 0x40004 (262148 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x2a (42 bytes) (User interface name section)
              Name: VarBlockServiceDxe
            File 8: fe5cea76-4f72-49e8-986f-2cd899dffe5d type 0x07, attr 0x00, state 0x07, size 0x8088 (32904 bytes), (driver)
              Section 0: type 0x13, size 0x3a (58 bytes) (DXE dependency expression section)
                PUSH 8f644fa9-e850-4db1-9ce2-0b44698e8da4
                PUSH b7dfb4e1-052f-449f-87be-9818fc91b733
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                AND
                AND
                END
              Section 1: type 0x10, size 0x8004 (32772 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x30 (48 bytes) (User interface name section)
              Name: FaultTolerantWriteDxe
            File 9: cbd2e4d5-7068-4ff5-b462-9822b4ad8d60 type 0x07, attr 0x00, state 0x07, size 0x4005e (262238 bytes), (driver)
              Section 0: type 0x13, size 0x16 (22 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                END
              Section 1: type 0x10, size 0x40004 (262148 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x2a (42 bytes) (User interface name section)
              Name: VariableRuntimeDxe
            File 10: ad608272-d07f-4964-801e-7bd3b7888652 type 0x07, attr 0x00, state 0x07, size 0x30092 (196754 bytes), (driver)
              Section 0: type 0x13, size 0x3a (58 bytes) (DXE dependency expression section)
                PUSH 1e5668e2-8481-11d4-bcf1-0080c73c8881
                PUSH 6441f818-6362-4e44-b570-7dba31dd2453
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                AND
                AND
                END
              Section 1: type 0x10, size 0x30004 (196612 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x3a (58 bytes) (User interface name section)
              Name: MonotonicCounterRuntimeDxe
            File 11: 16036a73-e8ef-46d0-953c-9b8e96527d13 type 0x07, attr 0x00, state 0x07, size 0x30044 (196676 bytes), (driver)
              Section 0: type 0x13, size 0x16 (22 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                END
              Section 1: type 0x10, size 0x30004 (196612 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x10 (16 bytes) (User interface name section)
              Name: Reset
            File 12: b336f62d-4135-4a55-ae4e-4971bbf0885d type 0x07, attr 0x00, state 0x07, size 0x30064 (196708 bytes), (driver)
              Section 0: type 0x13, size 0x28 (40 bytes) (DXE dependency expression section)
                PUSH 1e5668e2-8481-11d4-bcf1-0080c73c8881
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                AND
                END
              Section 1: type 0x10, size 0x30004 (196612 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x20 (32 bytes) (User interface name section)
              Name: RealTimeClock
            File 13: 4c6e0267-c77d-410d-8100-1495911a989d type 0x07, attr 0x00, state 0x07, size 0x5052 (20562 bytes), (driver)
              Section 0: type 0x13, size 0x16 (22 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                END
              Section 1: type 0x10, size 0x5004 (20484 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x1e (30 bytes) (User interface name section)
              Name: MetronomeDxe
            File 14: 348c4d62-bfbd-4882-9ece-c80bb1c4783b type 0x07, attr 0x00, state 0x07, size 0x1f050 (127056 bytes), (driver)
              Section 0: type 0x13, size 0x16 (22 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                END
              Section 1: type 0x10, size 0x1f004 (126980 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x1c (28 bytes) (User interface name section)
              Name: HiiDatabase
            File 15: 51ccf399-4fdf-4e55-a45b-e123f84d456a type 0x07, attr 0x00, state 0x07, size 0x803e (32830 bytes), (driver)
              Section 0: type 0x10, size 0x8004 (32772 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x22 (34 bytes) (User interface name section)
              Name: ConPlatformDxe
            File 16: 408edcec-cf6d-477c-a5a8-b4844e3de281 type 0x07, attr 0x00, state 0x07, size 0xb03e (45118 bytes), (driver)
              Section 0: type 0x10, size 0xb004 (45060 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x22 (34 bytes) (User interface name section)
              Name: ConSplitterDxe
            File 17: cccb0c28-4b24-11d5-9a5a-0090273fc14d type 0x07, attr 0x00, state 0x07, size 0x9046 (36934 bytes), (driver)
              Section 0: type 0x10, size 0x9004 (36868 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x2a (42 bytes) (User interface name section)
              Name: GraphicsConsoleDxe
            File 18: 9e863906-a40f-4875-977f-5b93ff237fc6 type 0x07, attr 0x00, state 0x07, size 0xb038 (45112 bytes), (driver)
              Section 0: type 0x10, size 0xb004 (45060 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x1c (28 bytes) (User interface name section)
              Name: TerminalDxe
            File 19: 9a5163e7-5c29-453f-825c-837a46a81e15 type 0x07, attr 0x00, state 0x07, size 0x605c (24668 bytes), (driver)
              Section 0: type 0x13, size 0x28 (40 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                PUSH 0aca9535-7ad0-4286-b02e-87fa7e2a5711
                AND
                END
              Section 1: type 0x10, size 0x6004 (24580 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x18 (24 bytes) (User interface name section)
              Name: SerialDxe
            File 20: c5deae31-fad2-4030-841b-cfc9644d2c5b type 0x07, attr 0x00, state 0x07, size 0x8126 (33062 bytes), (driver)
              Section 0: type 0x13, size 0xee (238 bytes) (DXE dependency expression section)
                PUSH 26baccb1-6f42-11d4-bce7-0080c73c8881
                PUSH 0aca9535-7ad0-4286-b02e-87fa7e2a5711
                PUSH 665e3ff6-46cc-11d4-9a38-0090273fc14d
                PUSH 26baccb2-6f42-11d4-bce7-0080c73c8881
                PUSH 1da97072-bddc-4b30-99f1-72a0b56fff2a
                PUSH 27cfac87-46cc-11d4-9a38-0090273fc14d
                PUSH 27cfac88-46cc-11d4-9a38-0090273fc14d
                PUSH b7dfb4e1-052f-449f-87be-9818fc91b733
                PUSH a46423e3-4617-49f1-b9ff-d1bfa9115839
                PUSH 26baccb3-6f42-11d4-bce7-0080c73c8881
                PUSH 6441f818-6362-4e44-b570-7dba31dd2453
                PUSH 1e5668e2-8481-11d4-bcf1-0080c73c8881
                PUSH 665e3ff5-46cc-11d4-9a38-0090273fc14d
                AND
                AND
                AND
                AND
                AND
                AND
                AND
                AND
                AND
                AND
                AND
                AND
                END
              Section 1: type 0x10, size 0x8004 (32772 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x1a (26 bytes) (User interface name section)
              Name: DisplayDxe
            File 21: bbe2668c-0efc-46fb-9137-4f2da8f419f3 type 0x07, attr 0x00, state 0x07, size 0x70e2 (28898 bytes), (driver)
              Section 0: type 0x13, size 0x70 (112 bytes) (DXE dependency expression section)
                PUSH 1e5668e2-8481-11d4-bcf1-0080c73c8881
                PUSH 6441f818-6362-4e44-b570-7dba31dd2453
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                PUSH 0fd96974-23aa-4cdc-b9cb-98d17750322a
                PUSH ef9fc172-a1b2-4693-b327-6d32fc416042
                PUSH 587e72d7-cc50-4f79-8209-ca291fc1a10f
                AND
                AND
                AND
                AND
                AND
                END
              Section 1: type 0x19, size 0x34 (52 bytes) (Raw section)
              Section 2: type 0x10, size 0x7004 (28676 bytes) (PE32 image section)
              Section 3: type 0x15, size 0x22 (34 bytes) (User interface name section)
              Name: ConsolePrefDxe
            File 22: de371f7c-dec4-4d21-adf1-593abcc15882 type 0x07, attr 0x00, state 0x07, size 0x704c (28748 bytes), (driver)
              Section 0: type 0x13, size 0x16 (22 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                END
              Section 1: type 0x10, size 0x7004 (28676 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x18 (24 bytes) (User interface name section)
              Name: ArmGicDxe
            File 23: 6d4628df-49a0-4b67-a325-d5af35c65745 type 0x07, attr 0x00, state 0x07, size 0x9066 (36966 bytes), (driver)
              Section 0: type 0x13, size 0x28 (40 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                PUSH 26baccb1-6f42-11d4-bce7-0080c73c8881
                AND
                END
              Section 1: type 0x10, size 0x9004 (36868 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x22 (34 bytes) (User interface name section)
              Name: RpiFirmwareDxe
            File 24: 8505280f-109e-437e-9fe4-1aa09c7074d9 type 0x07, attr 0x00, state 0x07, size 0x8056 (32854 bytes), (driver)
              Section 0: type 0x13, size 0x28 (40 bytes) (DXE dependency expression section)
                PUSH 0aca9535-7ad0-4286-b02e-87fa7e2a5711
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                AND
                END
              Section 1: type 0x10, size 0x8004 (32772 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x12 (18 bytes) (User interface name section)
              Name: FdtDxe
            File 25: 755cbac2-b23f-4b92-bc8e-fb01ce5907b7 type 0x07, attr 0x00, state 0x07, size 0xa0d8 (41176 bytes), (driver)
              Section 0: type 0x13, size 0x70 (112 bytes) (DXE dependency expression section)
                PUSH 11b34006-d85b-4d0a-a290-d5a571310ef7
                PUSH 0aca9535-7ad0-4286-b02e-87fa7e2a5711
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                PUSH 0fd96974-23aa-4cdc-b9cb-98d17750322a
                PUSH ef9fc172-a1b2-4693-b327-6d32fc416042
                PUSH 587e72d7-cc50-4f79-8209-ca291fc1a10f
                AND
                AND
                AND
                AND
                AND
                END
              Section 1: type 0x19, size 0x34 (52 bytes) (Raw section)
              Section 2: type 0x10, size 0xa004 (40964 bytes) (PE32 image section)
              Section 3: type 0x15, size 0x18 (24 bytes) (User interface name section)
              Name: ConfigDxe
            File 26: 49ea041e-6752-42ca-b0b1-7344fe2546b7 type 0x07, attr 0x00, state 0x07, size 0x6060 (24672 bytes), (driver)
              Section 0: type 0x13, size 0x28 (40 bytes) (DXE dependency expression section)
                PUSH 2890b3ea-053d-1643-ad0c-d64808da3ff1
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                AND
                END
              Section 1: type 0x10, size 0x6004 (24580 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x1c (28 bytes) (User interface name section)
              Name: ArmTimerDxe
            File 27: f099d67f-71ae-4c36-b2a3-dceb0eb2b7d8 type 0x07, attr 0x00, state 0x07, size 0x5064 (20580 bytes), (driver)
              Section 0: type 0x13, size 0x28 (40 bytes) (DXE dependency expression section)
                PUSH 26baccb3-6f42-11d4-bce7-0080c73c8881
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                AND
                END
              Section 1: type 0x10, size 0x5004 (20484 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x20 (32 bytes) (User interface name section)
              Name: WatchdogTimer
            File 28: 13ac6dd0-73d0-11d4-b06b-00aa00bd6de7 type 0x07, attr 0x00, state 0x07, size 0xa046 (41030 bytes), (driver)
              Section 0: type 0x13, size 0x16 (22 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                END
              Section 1: type 0x10, size 0xa004 (40964 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x12 (18 bytes) (User interface name section)
              Name: EbcDxe
            File 29: 6b38f7b4-ad98-40e9-9093-aca2b5a253c4 type 0x07, attr 0x00, state 0x07, size 0x8034 (32820 bytes), (driver)
              Section 0: type 0x10, size 0x8004 (32772 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x18 (24 bytes) (User interface name section)
              Name: DiskIoDxe
            File 30: 1fa1f39e-feff-4aae-bd7b-38a070a3b609 type 0x07, attr 0x00, state 0x07, size 0xa03a (41018 bytes), (driver)
              Section 0: type 0x10, size 0xa004 (40964 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x1e (30 bytes) (User interface name section)
              Name: PartitionDxe
            File 31: 961578fe-b6b7-44c3-af35-6bc705cd2b1f type 0x07, attr 0x00, state 0x07, size 0xe028 (57384 bytes), (driver)
              Section 0: type 0x10, size 0xe004 (57348 bytes) (PE32 image section)
              Section 1: type 0x15, size 0xc (12 bytes) (User interface name section)
              Name: Fat
            File 32: cd3bafb6-50fb-4fe8-8e4e-ab74d2c1a600 type 0x07, attr 0x00, state 0x07, size 0x5036 (20534 bytes), (driver)
              Section 0: type 0x10, size 0x5004 (20484 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x1a (26 bytes) (User interface name section)
              Name: EnglishDxe
            File 33: 7c04a583-9e3e-4f1c-ad65-e05268d0b4d1 type 0x09, attr 0x00, state 0x07, size 0xfc048 (1032264 bytes), (application)
              Section 0: type 0x15, size 0x10 (16 bytes) (User interface name section)
              Name: Shell
              Section 1: type 0x19, size 0x1c (28 bytes) (Raw section)
              Section 2: type 0x10, size 0xfc004 (1032196 bytes) (PE32 image section)
            File 34: 9622e42c-8e38-4a08-9e8f-54f784652f6b type 0x07, attr 0x00, state 0x07, size 0xb052 (45138 bytes), (driver)
              Section 0: type 0x13, size 0x16 (22 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                END
              Section 1: type 0x10, size 0xb004 (45060 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x1e (30 bytes) (User interface name section)
              Name: AcpiTableDxe
            File 35: b8e62775-bb0a-43f0-a843-5be8b14f8ccd type 0x07, attr 0x00, state 0x07, size 0x605a (24666 bytes), (driver)
              Section 0: type 0x10, size 0x6004 (24580 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x3e (62 bytes) (User interface name section)
              Name: BootGraphicsResourceTableDxe
            File 36: 7e374e25-8e01-4fee-87f2-390c23c606cd type 0x02, attr 0x00, state 0x07, size 0x3aa4 (15012 bytes), (freeform)
              Section 0: type 0x19, size 0x224 (548 bytes) (Raw section)
              Section 1: type 0x19, size 0x124 (292 bytes) (Raw section)
              Section 2: type 0x19, size 0x124 (292 bytes) (Raw section)
              Section 3: type 0x19, size 0x1c4 (452 bytes) (Raw section)
              Section 4: type 0x19, size 0x124 (292 bytes) (Raw section)
              Section 5: type 0x19, size 0x164 (356 bytes) (Raw section)
              Section 6: type 0x19, size 0x244 (580 bytes) (Raw section)
              Section 7: type 0x19, size 0x244 (580 bytes) (Raw section)
              Section 8: type 0x19, size 0x104 (260 bytes) (Raw section)
              Section 9: type 0x19, size 0x104 (260 bytes) (Raw section)
              Section 10: type 0x19, size 0x229c (8860 bytes) (Raw section)
              Section 11: type 0x19, size 0x27b (635 bytes) (Raw section)
              Section 12: type 0x19, size 0x298 (664 bytes) (Raw section)
              Section 13: type 0x19, size 0x14c (332 bytes) (Raw section)
              Section 14: type 0x19, size 0x248 (584 bytes) (Raw section)
            File 37: bad0554e-22e9-4d83-9afd-cc87727a1a45 type 0x07, attr 0x00, state 0x07, size 0x7080 (28800 bytes), (driver)
              Section 0: type 0x13, size 0x3a (58 bytes) (DXE dependency expression section)
                PUSH 03583ff6-cb36-4940-947e-b9b39f4afaf7
                PUSH 0aca9535-7ad0-4286-b02e-87fa7e2a5711
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                AND
                AND
                END
              Section 1: type 0x10, size 0x7004 (28676 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x28 (40 bytes) (User interface name section)
              Name: PlatformSmbiosDxe
            File 38: f9d88642-0737-49bc-81b5-6889cd57d9ea type 0x07, attr 0x00, state 0x07, size 0x804c (32844 bytes), (driver)
              Section 0: type 0x13, size 0x16 (22 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                END
              Section 1: type 0x10, size 0x8004 (32772 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x18 (24 bytes) (User interface name section)
              Name: SmbiosDxe
            File 39: 28a03ff4-12b3-4305-a417-bb1a4f94081e type 0x07, attr 0x00, state 0x07, size 0xe14c (57676 bytes), (driver)
              Section 0: type 0x13, size 0x5e (94 bytes) (DXE dependency expression section)
                PUSH 587e72d7-cc50-4f79-8209-ca291fc1a10f
                PUSH ef9fc172-a1b2-4693-b327-6d32fc416042
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                PUSH 0fd96974-23aa-4cdc-b9cb-98d17750322a
                PUSH b9d4c360-bcfb-4f9b-9298-53c136982258
                AND
                AND
                AND
                AND
                END
              Section 1: type 0x19, size 0x34 (52 bytes) (Raw section)
              Section 2: type 0x10, size 0xe004 (57348 bytes) (PE32 image section)
              Section 3: type 0x15, size 0x1a (26 bytes) (User interface name section)
              Name: RamDiskDxe
              Section 4: type 0x19, size 0x80 (128 bytes) (Raw section)
            File 40: e622443c-284e-4b47-a984-fd66b482dac0 type 0x07, attr 0x00, state 0x07, size 0x7096 (28822 bytes), (driver)
              Section 0: type 0x13, size 0x4c (76 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                PUSH 0fd96974-23aa-4cdc-b9cb-98d17750322a
                PUSH ef9fc172-a1b2-4693-b327-6d32fc416042
                PUSH 587e72d7-cc50-4f79-8209-ca291fc1a10f
                AND
                AND
                AND
                END
              Section 1: type 0x10, size 0x7004 (28676 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x2e (46 bytes) (User interface name section)
              Name: BootManagerPolicyDxe
            File 41: 9b680fce-ad6b-4f3a-b60b-f59899003443 type 0x07, attr 0x00, state 0x07, size 0xf054 (61524 bytes), (driver)
              Section 0: type 0x13, size 0x16 (22 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                END
              Section 1: type 0x10, size 0xf004 (61444 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x20 (32 bytes) (User interface name section)
              Name: DevicePathDxe
            File 42: e660ea85-058e-4b55-a54b-f02f83a24707 type 0x07, attr 0x00, state 0x07, size 0x170b8 (94392 bytes), (driver)
              Section 0: type 0x13, size 0x5e (94 bytes) (DXE dependency expression section)
                PUSH ef9fc172-a1b2-4693-b327-6d32fc416042
                PUSH 587e72d7-cc50-4f79-8209-ca291fc1a10f
                PUSH a770c357-b693-4e6d-a6cf-d21c728e550b
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                PUSH 0fd96974-23aa-4cdc-b9cb-98d17750322a
                AND
                AND
                AND
                AND
                END
              Section 1: type 0x19, size 0x1c (28 bytes) (Raw section)
              Section 2: type 0x10, size 0x17004 (94212 bytes) (PE32 image section)
              Section 3: type 0x15, size 0x20 (32 bytes) (User interface name section)
              Name: DisplayEngine
            File 43: ebf342fe-b1d3-4ef8-957c-8048606ff671 type 0x07, attr 0x00, state 0x07, size 0x1b086 (110726 bytes), (driver)
              Section 0: type 0x13, size 0x4c (76 bytes) (DXE dependency expression section)
                PUSH ef9fc172-a1b2-4693-b327-6d32fc416042
                PUSH 587e72d7-cc50-4f79-8209-ca291fc1a10f
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                PUSH 0fd96974-23aa-4cdc-b9cb-98d17750322a
                AND
                AND
                AND
                END
              Section 1: type 0x10, size 0x1b004 (110596 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x1e (30 bytes) (User interface name section)
              Name: SetupBrowser
            File 44: ebf8ed7c-0dd1-4787-84f1-f48d537dcacf type 0x07, attr 0x00, state 0x07, size 0xc0fa (49402 bytes), (driver)
              Section 0: type 0x13, size 0x5e (94 bytes) (DXE dependency expression section)
                PUSH ef9fc172-a1b2-4693-b327-6d32fc416042
                PUSH b9d4c360-bcfb-4f9b-9298-53c136982258
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                PUSH 0fd96974-23aa-4cdc-b9cb-98d17750322a
                PUSH 587e72d7-cc50-4f79-8209-ca291fc1a10f
                AND
                AND
                AND
                AND
                END
              Section 1: type 0x19, size 0x4c (76 bytes) (Raw section)
              Section 2: type 0x10, size 0xc004 (49156 bytes) (PE32 image section)
              Section 3: type 0x15, size 0x32 (50 bytes) (User interface name section)
              Name: DriverHealthManagerDxe
            File 45: 6d33944a-ec75-4855-a54d-809c75241f6c type 0x07, attr 0x00, state 0x07, size 0x1a07a (106618 bytes), (driver)
              Section 0: type 0x13, size 0x4c (76 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                PUSH 0fd96974-23aa-4cdc-b9cb-98d17750322a
                PUSH ef9fc172-a1b2-4693-b327-6d32fc416042
                PUSH 587e72d7-cc50-4f79-8209-ca291fc1a10f
                AND
                AND
                AND
                END
              Section 1: type 0x10, size 0x1a004 (106500 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x12 (18 bytes) (User interface name section)
              Name: BdsDxe
            File 46: 462caa21-7614-4503-836e-8ab6f4662331 type 0x09, attr 0x00, state 0x07, size 0x2a060 (172128 bytes), (application)
              Section 0: type 0x15, size 0x10 (16 bytes) (User interface name section)
              Name: UiApp
              Section 1: type 0x19, size 0x34 (52 bytes) (Raw section)
              Section 2: type 0x10, size 0x2a004 (172036 bytes) (PE32 image section)
            File 47: a210f973-229d-4f4d-aa37-9895e6c9eaba type 0x07, attr 0x00, state 0x07, size 0x5046 (20550 bytes), (driver)
              Section 0: type 0x13, size 0x16 (22 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                END
              Section 1: type 0x10, size 0x5004 (20484 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x12 (18 bytes) (User interface name section)
              Name: DpcDxe
            File 48: a2f436ea-a127-4ef8-957c-8048606ff670 type 0x07, attr 0x00, state 0x07, size 0xb02e (45102 bytes), (driver)
              Section 0: type 0x10, size 0xb004 (45060 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x12 (18 bytes) (User interface name section)
              Name: SnpDxe
            File 49: e4f61863-fe2c-4b56-a8f4-08519bc439df type 0x07, attr 0x00, state 0x07, size 0xa070 (41072 bytes), (driver)
              Section 0: type 0x19, size 0x34 (52 bytes) (Raw section)
              Section 1: type 0x10, size 0xa004 (40964 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x20 (32 bytes) (User interface name section)
              Name: VlanConfigDxe
            File 50: 025bbfc7-e6a9-4b8b-82ad-6815a1aeaf4a type 0x07, attr 0x00, state 0x07, size 0xf02e (61486 bytes), (driver)
              Section 0: type 0x10, size 0xf004 (61444 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x12 (18 bytes) (User interface name section)
              Name: MnpDxe
            File 51: 529d3f93-e8e9-4e73-b1e1-bdf6a9d50113 type 0x07, attr 0x00, state 0x07, size 0xa02e (41006 bytes), (driver)
              Section 0: type 0x10, size 0xa004 (40964 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x12 (18 bytes) (User interface name section)
              Name: ArpDxe
            File 52: 94734718-0bbc-47fb-96a5-ee7a5ae6a2ad type 0x07, attr 0x00, state 0x07, size 0xd032 (53298 bytes), (driver)
              Section 0: type 0x10, size 0xd004 (53252 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x16 (22 bytes) (User interface name section)
              Name: Dhcp4Dxe
            File 53: 9fb1a1f3-3b71-4324-b39a-745cbb015fff type 0x07, attr 0x00, state 0x07, size 0x16062 (90210 bytes), (driver)
              Section 0: type 0x19, size 0x34 (52 bytes) (Raw section)
              Section 1: type 0x10, size 0x16004 (90116 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x12 (18 bytes) (User interface name section)
              Name: Ip4Dxe
            File 54: 6d6963ab-906d-4a65-a7ca-bd40e5d6af2b type 0x07, attr 0x00, state 0x07, size 0xd030 (53296 bytes), (driver)
              Section 0: type 0x10, size 0xd004 (53252 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x14 (20 bytes) (User interface name section)
              Name: Udp4Dxe
            File 55: dc3641b8-2fa8-4ed3-bc1f-f9962a03454b type 0x07, attr 0x00, state 0x07, size 0xd034 (53300 bytes), (driver)
              Section 0: type 0x10, size 0xd004 (53252 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x18 (24 bytes) (User interface name section)
              Name: Mtftp4Dxe
            File 56: 95e3669d-34be-4775-a651-7ea41b69d89e type 0x07, attr 0x00, state 0x07, size 0xe032 (57394 bytes), (driver)
              Section 0: type 0x10, size 0xe004 (57348 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x16 (22 bytes) (User interface name section)
              Name: Dhcp6Dxe
            File 57: 5bedb5cc-d830-4eb2-8742-2d4cc9b54f2c type 0x07, attr 0x00, state 0x07, size 0x1f062 (127074 bytes), (driver)
              Section 0: type 0x19, size 0x34 (52 bytes) (Raw section)
              Section 1: type 0x10, size 0x1f004 (126980 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x12 (18 bytes) (User interface name section)
              Name: Ip6Dxe
            File 58: d912c7bc-f098-4367-92ba-e911083c7b0e type 0x07, attr 0x00, state 0x07, size 0xd030 (53296 bytes), (driver)
              Section 0: type 0x10, size 0xd004 (53252 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x14 (20 bytes) (User interface name section)
              Name: Udp6Dxe
            File 59: 99f03b99-98d8-49dd-a8d3-3219d0ffe41e type 0x07, attr 0x00, state 0x07, size 0xd034 (53300 bytes), (driver)
              Section 0: type 0x10, size 0xd004 (53252 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x18 (24 bytes) (User interface name section)
              Name: Mtftp6Dxe
            File 60: 1a7e4468-2f55-4a56-903c-01265eb7622b type 0x07, attr 0x00, state 0x07, size 0x1602e (90158 bytes), (driver)
              Section 0: type 0x10, size 0x16004 (90116 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x12 (18 bytes) (User interface name section)
              Name: TcpDxe
            File 61: b95e9fda-26de-48d2-8807-1f9107ac5e3a type 0x07, attr 0x00, state 0x07, size 0x1303a (77882 bytes), (driver)
              Section 0: type 0x10, size 0x13004 (77828 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x1e (30 bytes) (User interface name section)
              Name: UefiPxeBcDxe
            File 62: 3aceb0c0-3c72-11e4-9a56-74d435052646 type 0x07, attr 0x00, state 0x07, size 0xa311e (667934 bytes), (driver)
              Section 0: type 0x13, size 0xee (238 bytes) (DXE dependency expression section)
                PUSH 3152bca5-eade-433d-862e-c01cdc291f44
                PUSH 665e3ff6-46cc-11d4-9a38-0090273fc14d
                PUSH 26baccb1-6f42-11d4-bce7-0080c73c8881
                PUSH 26baccb2-6f42-11d4-bce7-0080c73c8881
                PUSH 1da97072-bddc-4b30-99f1-72a0b56fff2a
                PUSH 27cfac87-46cc-11d4-9a38-0090273fc14d
                PUSH 27cfac88-46cc-11d4-9a38-0090273fc14d
                PUSH b7dfb4e1-052f-449f-87be-9818fc91b733
                PUSH a46423e3-4617-49f1-b9ff-d1bfa9115839
                PUSH 26baccb3-6f42-11d4-bce7-0080c73c8881
                PUSH 6441f818-6362-4e44-b570-7dba31dd2453
                PUSH 1e5668e2-8481-11d4-bcf1-0080c73c8881
                PUSH 665e3ff5-46cc-11d4-9a38-0090273fc14d
                AND
                AND
                AND
                AND
                AND
                AND
                AND
                AND
                AND
                AND
                AND
                AND
                END
              Section 1: type 0x10, size 0xa3004 (667652 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x12 (18 bytes) (User interface name section)
              Name: TlsDxe
            File 63: 7ca1024f-eb17-11e5-9dba-28d2447c4829 type 0x07, attr 0x00, state 0x07, size 0x100d6 (65750 bytes), (driver)
              Section 0: type 0x13, size 0x5e (94 bytes) (DXE dependency expression section)
                PUSH 587e72d7-cc50-4f79-8209-ca291fc1a10f
                PUSH ef9fc172-a1b2-4693-b327-6d32fc416042
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                PUSH 0fd96974-23aa-4cdc-b9cb-98d17750322a
                PUSH b9d4c360-bcfb-4f9b-9298-53c136982258
                AND
                AND
                AND
                AND
                END
              Section 1: type 0x19, size 0x34 (52 bytes) (Raw section)
              Section 2: type 0x10, size 0x10004 (65540 bytes) (PE32 image section)
              Section 3: type 0x15, size 0x26 (38 bytes) (User interface name section)
              Name: TlsAuthConfigDxe
            File 64: b219e140-dffc-11e3-b956-0022681e6906 type 0x07, attr 0x00, state 0x07, size 0xf02e (61486 bytes), (driver)
              Section 0: type 0x10, size 0xf004 (61444 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x12 (18 bytes) (User interface name section)
              Name: DnsDxe
            File 65: 2366c20f-e15a-11e3-8bf1-e4115b28bc50 type 0x07, attr 0x00, state 0x07, size 0x10030 (65584 bytes), (driver)
              Section 0: type 0x10, size 0x10004 (65540 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x14 (20 bytes) (User interface name section)
              Name: HttpDxe
            File 66: 22ea234f-e72a-11e4-91f9-28d2447c4829 type 0x07, attr 0x00, state 0x07, size 0x605a (24666 bytes), (driver)
              Section 0: type 0x13, size 0x16 (22 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                END
              Section 1: type 0x10, size 0x6004 (24580 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x26 (38 bytes) (User interface name section)
              Name: HttpUtilitiesDxe
            File 67: ecebcb00-d9c8-11e4-af3d-8cdcd426c973 type 0x07, attr 0x00, state 0x07, size 0x1406c (82028 bytes), (driver)
              Section 0: type 0x19, size 0x34 (52 bytes) (Raw section)
              Section 1: type 0x10, size 0x14004 (81924 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x1c (28 bytes) (User interface name section)
              Name: HttpBootDxe
            File 68: e2b1eaf3-50b7-4ae1-b79e-ec8020cb57ac type 0x07, attr 0x00, state 0x07, size 0xa038 (41016 bytes), (driver)
              Section 0: type 0x10, size 0xa004 (40964 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x1c (28 bytes) (User interface name section)
              Name: BcmGenetDxe
            File 69: 5ec564ce-b656-435c-a652-5cb719784542 type 0x07, attr 0x00, state 0x07, size 0x6054 (24660 bytes), (driver)
              Section 0: type 0x13, size 0x16 (22 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                END
              Section 1: type 0x10, size 0x6004 (24580 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x20 (32 bytes) (User interface name section)
              Name: Bcm2838RngDxe
            File 70: 168d1a6e-f4a5-448a-9e95-795661bb3067 type 0x07, attr 0x00, state 0x07, size 0x6058 (24664 bytes), (driver)
              Section 0: type 0x13, size 0x16 (22 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                END
              Section 1: type 0x10, size 0x6004 (24580 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x24 (36 bytes) (User interface name section)
              Name: ArmPciCpuIo2Dxe
            File 71: 128fb770-5e79-4176-9e51-9bb268a17dd1 type 0x07, attr 0x00, state 0x07, size 0x1007e (65662 bytes), (driver)
              Section 0: type 0x13, size 0x3a (58 bytes) (DXE dependency expression section)
                PUSH ad61f191-ae5f-4c0e-b9fa-e869d288c64f
                PUSH 26baccb1-6f42-11d4-bce7-0080c73c8881
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                AND
                AND
                END
              Section 1: type 0x10, size 0x10004 (65540 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x26 (38 bytes) (User interface name section)
              Name: PciHostBridgeDxe
            File 72: 93b80004-9fb3-11d4-9a3a-0090273fc14d type 0x07, attr 0x00, state 0x07, size 0x15034 (86068 bytes), (driver)
              Section 0: type 0x10, size 0x15004 (86020 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x18 (24 bytes) (User interface name section)
              Name: PciBusDxe
            File 73: 7ed510aa-9cdc-49d2-a306-6e11e359f9b3 type 0x07, attr 0x00, state 0x07, size 0x7070 (28784 bytes), (driver)
              Section 0: type 0x13, size 0x28 (40 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                PUSH 26baccb1-6f42-11d4-bce7-0080c73c8881
                AND
                END
              Section 1: type 0x10, size 0x7004 (28676 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x2c (44 bytes) (User interface name section)
              Name: NonCoherentIoMmuDxe
            File 74: 5be3bdf4-53cf-46a3-a6a9-73c34a6e5ee3 type 0x07, attr 0x00, state 0x07, size 0xd03c (53308 bytes), (driver)
              Section 0: type 0x10, size 0xd004 (53252 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x20 (32 bytes) (User interface name section)
              Name: NvmExpressDxe
            File 75: 0167ccc4-d0f7-4f21-a3ef-9e64b7cdce8b type 0x07, attr 0x00, state 0x07, size 0x8030 (32816 bytes), (driver)
              Section 0: type 0x10, size 0x8004 (32772 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x14 (20 bytes) (User interface name section)
              Name: ScsiBus
            File 76: 0a66e322-3740-4cce-ad62-bd172cecca35 type 0x07, attr 0x00, state 0x07, size 0xd032 (53298 bytes), (driver)
              Section 0: type 0x10, size 0xd004 (53252 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x16 (22 bytes) (User interface name section)
              Name: ScsiDisk
            File 77: b7f50e91-a759-412c-ade4-dcd03e7f7c28 type 0x07, attr 0x00, state 0x07, size 0x11030 (69680 bytes), (driver)
              Section 0: type 0x10, size 0x11004 (69636 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x14 (20 bytes) (User interface name section)
              Name: XhciDxe
            File 78: 4bf1704c-03f4-46d5-bca6-82fa580badfd type 0x07, attr 0x00, state 0x07, size 0xa12a (41258 bytes), (driver)
              Section 0: type 0x13, size 0xee (238 bytes) (DXE dependency expression section)
                PUSH 0aca9535-7ad0-4286-b02e-87fa7e2a5711
                PUSH 665e3ff6-46cc-11d4-9a38-0090273fc14d
                PUSH 26baccb1-6f42-11d4-bce7-0080c73c8881
                PUSH 26baccb2-6f42-11d4-bce7-0080c73c8881
                PUSH 1da97072-bddc-4b30-99f1-72a0b56fff2a
                PUSH 27cfac87-46cc-11d4-9a38-0090273fc14d
                PUSH 27cfac88-46cc-11d4-9a38-0090273fc14d
                PUSH b7dfb4e1-052f-449f-87be-9818fc91b733
                PUSH a46423e3-4617-49f1-b9ff-d1bfa9115839
                PUSH 26baccb3-6f42-11d4-bce7-0080c73c8881
                PUSH 6441f818-6362-4e44-b570-7dba31dd2453
                PUSH 1e5668e2-8481-11d4-bcf1-0080c73c8881
                PUSH 665e3ff5-46cc-11d4-9a38-0090273fc14d
                AND
                AND
                AND
                AND
                AND
                AND
                AND
                AND
                AND
                AND
                AND
                AND
                END
              Section 1: type 0x10, size 0xa004 (40964 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x1e (30 bytes) (User interface name section)
              Name: DwUsbHostDxe
            File 79: 240612b7-a063-11d4-9a3a-0090273fc14d type 0x07, attr 0x00, state 0x07, size 0xd034 (53300 bytes), (driver)
              Section 0: type 0x10, size 0xd004 (53252 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x18 (24 bytes) (User interface name section)
              Name: UsbBusDxe
            File 80: 2d2e62cf-9ecf-43b7-8219-94e7fc713dfe type 0x07, attr 0x00, state 0x07, size 0x9032 (36914 bytes), (driver)
              Section 0: type 0x10, size 0x9004 (36868 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x16 (22 bytes) (User interface name section)
              Name: UsbKbDxe
            File 81: 9fb4b4a7-42c0-4bcd-8540-9bcc6711f83e type 0x07, attr 0x00, state 0x07, size 0xa044 (41028 bytes), (driver)
              Section 0: type 0x10, size 0xa004 (40964 bytes) (PE32 image section)
              Section 1: type 0x15, size 0x28 (40 bytes) (User interface name section)
              Name: UsbMassStorageDxe
            File 82: 100c2cfa-b586-4198-9b4c-1683d195b1da type 0x07, attr 0x00, state 0x07, size 0x8088 (32904 bytes), (driver)
              Section 0: type 0x13, size 0x4c (76 bytes) (DXE dependency expression section)
                PUSH 0aca9535-7ad0-4286-b02e-87fa7e2a5711
                PUSH 0aca4444-7ad0-4286-b02e-87fa7e2a5711
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                PUSH 26baccb1-6f42-11d4-bce7-0080c73c8881
                AND
                AND
                AND
                END
              Section 1: type 0x10, size 0x8004 (32772 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x20 (32 bytes) (User interface name section)
              Name: ArasanMMCHost
            File 83: b6f44cc0-9e45-11df-be21-0002a5f5f51b type 0x07, attr 0x00, state 0x07, size 0xc046 (49222 bytes), (driver)
              Section 0: type 0x13, size 0x16 (22 bytes) (DXE dependency expression section)
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                END
              Section 1: type 0x10, size 0xc004 (49156 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x12 (18 bytes) (User interface name section)
              Name: MmcDxe
            File 84: f74d20ee-37e7-48fc-97f7-9b1047749c69 type 0x07, attr 0x00, state 0x07, size 0x3206c (204908 bytes), (driver)
              Section 0: type 0x13, size 0x3a (58 bytes) (DXE dependency expression section)
                PUSH ef9fc172-a1b2-4693-b327-6d32fc416042
                PUSH 1a1241e6-8f19-41a9-bc0e-e8ef39e06546
                PUSH 13a3f0f6-264a-3ef0-f2e0-dec512342f34
                AND
                AND
                END
              Section 1: type 0x10, size 0x32004 (204804 bytes) (PE32 image section)
              Section 2: type 0x15, size 0x14 (20 bytes) (User interface name section)
              Name: LogoDxe
Found volume magic at 0x1d0000
Firmware Volume: fff12b8d-7696-4c8b-a985-2747075b4f50 attr 0x0004feff, rev 2, cksum 0xf919, size 0x20000 (131072 bytes)
  Firmware Volume Blocks: (32, 0x1000)
  Raw section: NVRAM
```

### boot kernel from UEFI Shell

ref:

- https://www.kernel.org/doc/Documentation/efi-stub.txt
- https://wiki.debian.org/UEFI
- https://forums.raspberrypi.com/viewtopic.php?t=278791
- https://www.kernel.org/doc/html/v4.14/admin-guide/kernel-parameters.html
    - `man kernel-command-line`
    - `man bootparam`
    - `man initrd`
- https://www.kernel.org/doc/html/v4.14/admin-guide/initrd.html
- http://weng-blog.com/2017/07/21/ARMv8-UEFI-manual-boot.html
- http://wiki.espressobin.net/tiki-index.php?page=Creating+Ubuntu+filesystem
- https://cateee.net/lkddb/web-lkddb/EFI_PARAMS_FROM_FDT.html

Download `ubuntu-20.04.3-live-server-arm64.iso`, copy `vmlinux` and `initrd` to a folder in `ESP`:

```
$ wget https://cdimage.ubuntu.com/releases/20.04/release/ubuntu-20.04.3-live-server-arm64.iso
$ sudo mount ubuntu-20.04.3-live-server-arm64.iso /mnt
$ zcat /mnt/casper/vmlinuz > /ESP/u2004/vmlinux
$ cp /mnt/casper/initrd /ESP/u2004/initrm
```

#### no `initrd`

Then after boot into UEFI Shell:

```
InstallProtocolInterface: 387477C2-69C7-11D2-8E39-00A0C969723B 35870E20
InstallProtocolInterface: 752F3136-4E16-4FDC-A22A-E5F46812F4CA 35870C98
InstallProtocolInterface: 6302D008-7F9B-4F30-87AC-60C9FEF5DA4E 3389B9F0
UEFI Interactive Shell v2.2
EDK II
UEFI v2.70 (EDK2, 0x00010000)
Mapping table
      FS0: Alias(s):HD0a0a0b:;BLK1:
          PcieRoot(0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/USB(0x0,0x0)/USB(0x0,0x0)/HD(1
,MBR,0x04EA7D7A,0x800,0x100000)
     BLK2: Alias(s):
          VenHw(100C2CFA-B586-4198-9B4C-1683D195B1DA)
     BLK0: Alias(s):
          PcieRoot(0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/USB(0x0,0x0)/USB(0x0,0x0)
Press ESC in 3 seconds to skip startup.nsh or any other key to continue.
Shell> fs0:
FS0:\> dir
Directory of: FS0:\
10/19/2021  19:06              49,829  bcm2711-rpi-4-b.dtb
10/19/2021  18:57                 206  config.txt
10/19/2021  19:06               5,351  fixup4.dat
10/19/2021  19:06 <DIR>         4,096  overlays
10/19/2021  18:57               5,067  Readme.md
10/19/2021  19:05           2,031,616  RPI_EFI.fd
10/19/2021  19:06           2,031,616  RPI_EFI.fd-1.32
10/19/2021  19:06           2,243,232  start4.elf
10/20/2021  01:18                  42  test.nsh
10/25/2021  15:13 <DIR>         4,096  u2004
          8 File(s)   6,366,959 bytes
          2 Dir(s)
FS0:\> cd u2004
FS0:\u2004\> dir
Directory of: FS0:\u2004\
10/25/2021  15:13 <DIR>         4,096  .
10/25/2021  15:13 <DIR>             0  ..
10/25/2021  15:14          87,211,682  initrd
10/25/2021  15:11          30,544,256  vmlinux
10/25/2021  15:10          10,713,867  vmlinuz
          3 File(s)  128,469,805 bytes
          2 Dir(s)
FS0:\u2004\> vmlinux
[Security] 3rd party image[0] can be loaded after EndOfDxe: PcieRoot(0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/USB(0x0,0x0)/USB(0x0,0x0)/HD(1,MBR,0x04EA7D7A,0x800,0x100000)/\u2004\vmlinux.
InstallProtocolInterface: 5B1B31A1-9562-11D2-8E3F-00A0C969723B 35814040
Loading driver at 0x0002FB91000 EntryPoint=0x00030FC7618
Loading driver at 0x0002FB91000 EntryPoint=0x00030FC7618
Variables not dirty, not dumping!
InstallProtocolInterface: BC62157E-3E33-4FEC-9920-2D3B36D750DF 35828298
ProtectUefiImageCommon - 0x35814040
  - 0x000000002FB91000 - 0x0000000001E3D000
InstallProtocolInterface: 752F3136-4E16-4FDC-A22A-E5F46812F4CA 3B2FEEF8
EFI stub: Booting Linux Kernel...
EFI stub: Generating empty DTB
EFI stub: Exiting boot services and installing virtual address map...
XhcClearBiosOwnership: called to clear BIOS ownership
SetUefiImageMemoryAttributes - 0x0000000037160000 - 0x0000000000040000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x0000000033DF0000 - 0x0000000000040000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x0000000033DA0000 - 0x0000000000040000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x0000000037120000 - 0x0000000000030000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x0000000033D30000 - 0x0000000000030000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x0000000033CF0000 - 0x0000000000030000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x0000000033CB0000 - 0x0000000000030000 (0x0000000000000008)
[    0.000000] Booting Linux on physical CPU 0x0000000000 [0x410fd083]
[    0.000000] Linux version 5.4.0-81-generic (buildd@bos02-arm64-028) (gcc version 9.3.0 (Ubuntu 9.3.0-17ubuntu1~20.04)) #91-Ubuntu SMP Thu Jul 15 19:10:30 UTC 2021 (Ubuntu 5.4.0-81.91-generic 5.4.128)
[    0.000000] efi: Getting EFI parameters from FDT:
[    0.000000] efi: EFI v2.70 by EDK2
[    0.000000] efi:  ACPI 2.0=0x33d70018  SMBIOS=0x371c0000  SMBIOS 3.0=0x33c90000  MEMATTR=0x35814518  RNG=0x372dd098  MEMRESERVE=0x33e43018
[    0.000000] efi: seeding entropy pool
[    0.000000] random: fast init done
[    0.000000] secureboot: Secure boot disabled
[    0.000000] cma: Reserved 32 MiB at 0x000000007a000000
[    0.000000] ACPI: Early table checksum verification disabled
[    0.000000] ACPI: RSDP 0x0000000033D70018 000024 (v02 RPIFDN)
[    0.000000] ACPI: XSDT 0x0000000033D7FE98 00006C (v01 RPIFDN RPI4     00000200      01000013)
[    0.000000] ACPI: FACP 0x0000000033D7E998 000114 (v06 RPIFDN RPI4     00000200 EDK2 00000300)
[    0.000000] ACPI: DSDT 0x0000000033D77518 002298 (v02 RPIFDN RPI      00000002 INTL 20190509)
[    0.000000] ACPI: CSRT 0x0000000033D7FA98 000169 (v00 RPIFDN RPI4     00000200 EDK2 00000300)
[    0.000000] ACPI: DBG2 0x0000000033D7FD18 000061 (v00 RPIFDN RPI4     00000200 EDK2 00000300)
[    0.000000] ACPI: GTDT 0x0000000033D7F998 000068 (v03 RPIFDN RPI4     00000200 EDK2 00000300)
[    0.000000] ACPI: APIC 0x0000000033D7F598 000184 (v05 RPIFDN RPI4     00000200 EDK2 00000300)
[    0.000000] ACPI: PPTT 0x0000000033D7EB18 000184 (v02 RPIFDN RPI4     00000200 EDK2 00000300)
[    0.000000] ACPI: SPCR 0x0000000033D7FE18 000050 (v02 RPIFDN RPI4     00000200 EDK2 00000300)
[    0.000000] ACPI: SSDT 0x0000000033D7ED98 000277 (v02 RPIFDN RPI4EMMC 00000002 INTL 20190509)
[    0.000000] ACPI: SSDT 0x0000000033D7F198 000244 (v05 RPIFDN RPI4XHCI 00000002 INTL 20190509)
[    0.000000] ACPI: SPCR: console: pl011,mmio32,0xfe201000,115200
[    0.000000] ACPI: NUMA: Failed to initialise from firmware
[    0.000000] NUMA: Faking a node at [mem 0x0000000000000000-0x000000007fffffff]
[    0.000000] NUMA: NODE_DATA [mem 0x7fc21f40-0x7fc24fff]
...
[    1.593665] VFS: Cannot open root device "(null)" or unknown-block(0,0): error -6
[    1.601145] Please append a correct "root=" boot option; here are the available partitions:
[    1.609492] Kernel panic - not syncing: VFS: Unable to mount root fs on unknown-block(0,0)
[    1.617742] CPU: 3 PID: 1 Comm: swapper/0 Not tainted 5.4.0-81-generic #91-Ubuntu
[    1.625208] Hardware name: Raspberry Pi Foundation Raspberry Pi 4 Model B/Raspberry Pi 4 Model B, BIOS EDK2-DEV 10/20/2021
[    1.636232] Call trace:
[    1.638672]  dump_backtrace+0x0/0x190
[    1.642322]  show_stack+0x28/0x38
[    1.645626]  dump_stack+0xb4/0x10c
[    1.649016]  panic+0x150/0x364
[    1.652059]  mount_block_root+0x248/0x304
[    1.656055]  mount_root+0x48/0x50
[    1.659356]  prepare_namespace+0x13c/0x1bc
[    1.663438]  kernel_init_freeable+0x27c/0x2d0
[    1.667781]  kernel_init+0x1c/0x114
[    1.671257]  ret_from_fork+0x10/0x18
[    1.674822] SMP: stopping secondary CPUs
[    1.678735] Kernel Offset: 0x2c6f03b40000 from 0xffff800010000000
[    1.684813] PHYS_OFFSET: 0xffffbd7580000000
[    1.688982] CPU features: 0x0002,20806000
[    1.692976] Memory Limit: none
[    1.690314] Memory Limit: none
[    1.693358] ---[ end Kernel panic - not syncing: VFS: Unable to mount root fs on unknown-block(0,0) ]---
```

#### with `initrd`

如果在命令行上加 `initrd=\u2004\initrd` (according to [UEFI stub](https://www.kernel.org/doc/Documentation/efi-stub.txt), the `initrd` image is loaded by the "UEFI stub", where the stub assumes the role of bootloader):

```
FS0:\u2004\> vmlinux initrd=\u2004\initrd
...
[    5.240772]    8regs     :  5767.000 MB/sec
[    5.284771]    32regs    :  6756.000 MB/sec
[    5.328771]    arm64_neon:  6070.000 MB/sec
[    5.332944] xor: using function: 32regs (6756.000 MB/sec)
[    5.340271] async_tx: api initialized (async)
[    5.368944]  sda: sda1
[    5.374550] sd 0:0:0:0: [sda] Attached SCSI removable disk
done.
Begin: Running /scripts/init-premount ... done.
Begin: Mounting root file system ... Begin: Running /scripts/nfs-top ... done.
Begin: Running /scripts/nfs-premount ... done.
Begin: Running /scripts/casper-premount ... done.
done.
[   16.593922] random: crng init done
[   16.597327] random: 7 urandom warning(s) missed due to ratelimiting
Unable to find a medium container a live file system
Attempt interactive netboot from a URL?
yes no (default yes): no

BusyBox v1.30.1 (Ubuntu 1:1.30.1-4ubuntu6.3) built-in shell (ash)
Enter 'help' for a list of built-in commands.

(initramfs) Unable to find a medium containing a live file system

(initramfs) ls
dev          cryptroot    run          var          cdrom
root         etc          sbin         sys          casper.vars
bin          init         scripts      proc         casper.log
conf         lib          usr          tmp
(initramfs)
```

#### with `initrd` and `root`

Populate a rootfs on USB stick, according to <http://wiki.espressobin.net/tiki-index.php?page=Creating+Ubuntu+filesystem#Ubuntu_16.04.4_LTS> (using `unsquashfs`):

```
$ sudo fdist /dev/sdc   <== 1st partition is ESP(FAT32); now create the 2nd partition (Ext4)
$ sudo mkfs.ext4 /dev/sdc2
$ sudo mount /dev/sdc2 ~/distro/rootfs
$ sudo unsquashfs -d ~/distro/rootfs -f /mnt/casper/filesystem.squashfs
Parallel unsquashfs: Using 4 processors
33096 inodes (37416 blocks) to write
[===================================================================-] 37416/37416 100%
created 29470 files
created 3631 directories
created 3505 symlinks
created 9 devices
created 0 fifos
$ ls -la ~/distro/rootfs
total 88
drwxr-xr-x 19 root  root   4096 8月  24 16:49 .
drwxrwxr-x  3 bruin bruin  4096 10月 25 16:48 ..
lrwxrwxrwx  1 root  root      7 8月  24 16:43 bin -> usr/bin
drwxr-xr-x  2 root  root   4096 4月  15  2020 boot
drwxr-xr-x  5 root  root   4096 8月  24 16:46 dev
drwxr-xr-x 91 root  root   4096 8月  24 16:48 etc
drwxr-xr-x  2 root  root   4096 4月  15  2020 home
lrwxrwxrwx  1 root  root      7 8月  24 16:43 lib -> usr/lib
drwx------  2 root  root  16384 10月 25 16:47 lost+found
drwxr-xr-x  2 root  root   4096 8月  24 16:43 media
drwxr-xr-x  2 root  root   4096 8月  24 16:43 mnt
drwxr-xr-x  2 root  root   4096 8月  24 16:43 opt
drwxr-xr-x  2 root  root   4096 4月  15  2020 proc
drwx------  2 root  root   4096 8月  24 16:47 root
drwxr-xr-x 11 root  root   4096 8月  24 16:48 run
lrwxrwxrwx  1 root  root      8 8月  24 16:43 sbin -> usr/sbin
drwxr-xr-x  6 root  root   4096 8月  24 16:48 snap
drwxr-xr-x  2 root  root   4096 8月  24 16:43 srv
drwxr-xr-x  2 root  root   4096 4月  15  2020 sys
drwxrwxrwt  2 root  root   4096 8月  24 16:48 tmp
drwxr-xr-x 12 root  root   4096 8月  24 16:46 usr
drwxr-xr-x 13 root  root   4096 8月  24 16:47 var
$ sudo umount ~/distro/rootfs
```

FIXME: but booting from UEFI Shell with both `initrd` and `root` parameters gives the same result as only with `initrd` parameter (tried both `filesystem.squashfs` and `installer.squashfs` as rootfs). why?

#### with `root` only

看起来还是需要`initrd`中的驱动才能认识`/dev/sda2`:

```
FS0:\u2004\> vmlinux root=/dev/sda2
...
[    1.592202] VFS: Cannot open root device "sda2" or unknown-block(0,0): error -6
[    1.599503] Please append a correct "root=" boot option; here are the available partitions:
[    1.607851] Kernel panic - not syncing: VFS: Unable to mount root fs on unknown-block(0,0)
[    1.616101] CPU: 2 PID: 1 Comm: swapper/0 Not tainted 5.4.0-81-generic #91-Ubuntu
[    1.623567] Hardware name: Raspberry Pi Foundation Raspberry Pi 4 Model B/Raspberry Pi 4 Model B, BIOS EDK2-DEV 10/20/2021
[    1.634590] Call trace:
[    1.637030]  dump_backtrace+0x0/0x190
[    1.640680]  show_stack+0x28/0x38
[    1.643985]  dump_stack+0xb4/0x10c
[    1.647374]  panic+0x150/0x364
[    1.650417]  mount_block_root+0x248/0x304
[    1.654412]  mount_root+0x48/0x50
[    1.657713]  prepare_namespace+0x13c/0x1bc
[    1.661795]  kernel_init_freeable+0x27c/0x2d0
[    1.666138]  kernel_init+0x1c/0x114
[    1.669614]  ret_from_fork+0x10/0x18
[    1.673180] SMP: stopping secondary CPUs
[    1.677093] Kernel Offset: 0x41c200af0000 from 0xffff800010000000
[    1.683171] PHYS_OFFSET: 0xffffe62ec0000000
[    1.687340] CPU features: 0x0002,20806000
[    1.691335] Memory Limit: none
[    1.694379] ---[ end Kernel panic - not syncing: VFS: Unable to mount root fs on unknown-block(0,0) ]---
```

#### with `initrd`, `root` and `init`

ref:

- `init=/bin/bash`: https://raspberrypi.stackexchange.com/a/44950/140258
- `启动过程中initrd的作用`: https://blog.csdn.net/Ropyn/article/details/2489945
- [Linux System Process Initialization](http://glennastory.net/boot/initrd.html)

症状同前, `init=/bin/bash`没有起作用。通过查看log, 发现kernel总是会先执行`initrd`中的`init`脚本:

```
[    2.587512] Checked W+X mappings: passed, no W+X pages found
[    2.593184] Run /init as init process        <== 执行 initrd 中的 init脚本; cmdline 可以从 `/proc/cmdline` 获得
Loading, please wait...                         <== 脚本中的打印
```

可能这个 iso 是live cd, 所以它的init脚本是为安装准备的。

- https://cdimage.ubuntu.com/releases/20.04.3/release/ubuntu-20.04.3-preinstalled-server-arm64+raspi.img.xz
- https://ubuntu.com/tutorials/how-to-install-ubuntu-on-your-raspberry-pi#1-overview

## EDK2 for Qemu

### Install `qemu-system-arm`

ref:

- [FVP vs QEMU](https://stackoverflow.com/questions/53559478/qemu-and-fvp-models-difference/56135601#56135601)
- [为QEMU创建基于UEFI的AARCH64虚拟机](https://blog.csdn.net/fastboy_abc/article/details/86635638)

Choices:

- system mode vs user mode emulation: system mode => install `qemu-system-arm`
- machine: `virt` => `qemu-system-aa64 -M virt`
- cpu: `cortex-a72` => `qemu-system-aa64 -cpu cortex-a57`

QEMU can run in two modes: user mode and system mode. User mode allows you to run non-native binaries on your host OS (e.g. running a MIPS binary on an x64 system). System mode acts like a more traditional hypervisor where it emulates the underlying hardware and virtualizes the guest OS.

`qemu-system-arm` supported machines include `virt`, whose firmware is also supported by `edk2` (`ArmVirtPkg` pkg produces `QEMU_EFI.fd` firmware).

```
$ apt-cache show qemu
$ apt-cache show qemu-system-arm
$ sudo apt install qemu-system-arm
$ qemu-system-aarch64 --version
QEMU emulator version 4.2.1 (Debian 1:4.2-3ubuntu6.18)
Copyright (c) 2003-2019 Fabrice Bellard and the QEMU Project developers
$ qemu-system-aarch64 -M ?
Supported machines are:
akita                Sharp SL-C1000 (Akita) PDA (PXA270)
ast2500-evb          Aspeed AST2500 EVB (ARM1176)
ast2600-evb          Aspeed AST2600 EVB (Cortex A7)
borzoi               Sharp SL-C3100 (Borzoi) PDA (PXA270)
canon-a1100          Canon PowerShot A1100 IS
cheetah              Palm Tungsten|E aka. Cheetah PDA (OMAP310)
collie               Sharp SL-5500 (Collie) PDA (SA-1110)
connex               Gumstix Connex (PXA255)
cubieboard           cubietech cubieboard (Cortex-A8)
emcraft-sf2          SmartFusion2 SOM kit from Emcraft (M2S010)
highbank             Calxeda Highbank (ECX-1000)
imx25-pdk            ARM i.MX25 PDK board (ARM926)
integratorcp         ARM Integrator/CP (ARM926EJ-S)
kzm                  ARM KZM Emulation Baseboard (ARM1136)
lm3s6965evb          Stellaris LM3S6965EVB
lm3s811evb           Stellaris LM3S811EVB
mainstone            Mainstone II (PXA27x)
mcimx6ul-evk         Freescale i.MX6UL Evaluation Kit (Cortex A7)
mcimx7d-sabre        Freescale i.MX7 DUAL SABRE (Cortex A7)
microbit             BBC micro:bit
midway               Calxeda Midway (ECX-2000)
mps2-an385           ARM MPS2 with AN385 FPGA image for Cortex-M3
mps2-an505           ARM MPS2 with AN505 FPGA image for Cortex-M33
mps2-an511           ARM MPS2 with AN511 DesignStart FPGA image for Cortex-M3
mps2-an521           ARM MPS2 with AN521 FPGA image for dual Cortex-M33
musca-a              ARM Musca-A board (dual Cortex-M33)
musca-b1             ARM Musca-B1 board (dual Cortex-M33)
musicpal             Marvell 88w8618 / MusicPal (ARM926EJ-S)
n800                 Nokia N800 tablet aka. RX-34 (OMAP2420)
n810                 Nokia N810 tablet aka. RX-44 (OMAP2420)
netduino2            Netduino 2 Machine
none                 empty machine
nuri                 Samsung NURI board (Exynos4210)
palmetto-bmc         OpenPOWER Palmetto BMC (ARM926EJ-S)
raspi2               Raspberry Pi 2
raspi3               Raspberry Pi 3
realview-eb          ARM RealView Emulation Baseboard (ARM926EJ-S)
realview-eb-mpcore   ARM RealView Emulation Baseboard (ARM11MPCore)
realview-pb-a8       ARM RealView Platform Baseboard for Cortex-A8
realview-pbx-a9      ARM RealView Platform Baseboard Explore for Cortex-A9
romulus-bmc          OpenPOWER Romulus BMC (ARM1176)
sabrelite            Freescale i.MX6 Quad SABRE Lite Board (Cortex A9)
sbsa-ref             QEMU 'SBSA Reference' ARM Virtual Machine
smdkc210             Samsung SMDKC210 board (Exynos4210)
spitz                Sharp SL-C3000 (Spitz) PDA (PXA270)
swift-bmc            OpenPOWER Swift BMC (ARM1176)
sx1                  Siemens SX1 (OMAP310) V2
sx1-v1               Siemens SX1 (OMAP310) V1
terrier              Sharp SL-C3200 (Terrier) PDA (PXA270)
tosa                 Sharp SL-6000 (Tosa) PDA (PXA255)
verdex               Gumstix Verdex (PXA270)
versatileab          ARM Versatile/AB (ARM926EJ-S)
versatilepb          ARM Versatile/PB (ARM926EJ-S)
vexpress-a15         ARM Versatile Express for Cortex-A15
vexpress-a9          ARM Versatile Express for Cortex-A9
virt-2.10            QEMU 2.10 ARM Virtual Machine
virt-2.11            QEMU 2.11 ARM Virtual Machine
virt-2.12            QEMU 2.12 ARM Virtual Machine
virt-2.6             QEMU 2.6 ARM Virtual Machine
virt-2.7             QEMU 2.7 ARM Virtual Machine
virt-2.8             QEMU 2.8 ARM Virtual Machine
virt-2.9             QEMU 2.9 ARM Virtual Machine
virt-3.0             QEMU 3.0 ARM Virtual Machine
virt-3.1             QEMU 3.1 ARM Virtual Machine
virt-4.0             QEMU 4.0 ARM Virtual Machine
virt-4.1             QEMU 4.1 ARM Virtual Machine
virt                 QEMU 4.2 ARM Virtual Machine (alias of virt-4.2)
virt-4.2             QEMU 4.2 ARM Virtual Machine
witherspoon-bmc      OpenPOWER Witherspoon BMC (ARM1176)
xilinx-zynq-a9       Xilinx Zynq Platform Baseboard for Cortex-A9
xlnx-versal-virt     Xilinx Versal Virtual development board
xlnx-zcu102          Xilinx ZynqMP ZCU102 board with 4xA53s and 2xR5Fs based on the value of smp
z2                   Zipit Z2 (PXA27x)
$ qemu-system-aarch64 -M virt -cpu ?
Available CPUs:
  arm1026
  arm1136
  arm1136-r2
  arm1176
  arm11mpcore
  arm926
  arm946
  cortex-a15
  cortex-a53
  cortex-a57
  cortex-a7
  cortex-a72
  cortex-a8
  cortex-a9
  cortex-m0
  cortex-m3
  cortex-m33
  cortex-m4
  cortex-r5
  cortex-r5f
  max
  pxa250
  pxa255
  pxa260
  pxa261
  pxa262
  pxa270-a0
  pxa270-a1
  pxa270
  pxa270-b0
  pxa270-b1
  pxa270-c0
  pxa270-c5
  sa1100
  sa1110
  ti925t
```

### Build `QEMU_EFI.fd`

```
echo "Building ArmVirtPkg/ArmVirtQemu.dsc..."
GCC5_AARCH64_PREFIX=aarch64-none-linux-gnu- build \
      -n 4 \
      -a AARCH64 \
      -p ArmVirtPkg/ArmVirtQemu.dsc \
      -t GCC5 \
      -b DEBUG \
      all
```

The result is `Build/ArmVirtQemu-AARCH64/DEBUG_GCC5/FV/QEMU_EFI.fd`.

### Create VM

```
#!/bin/bash

mkdir -p ~/work/tianocore/hda-content
# cp `initrd` and `vmlinux` (after zcat) into `hda-content/`
qemu-system-aarch64 \
    -M virt \
    -cpu cortex-a72 \
    -bios /home/bruin/work/tianocore/Build/ArmVirtQemu-AARCH64/DEBUG_GCC5/FV/QEMU_EFI.fd \
    -hda fat:rw:hda-content/ \
    -net none

# select `View->serial0` to enter UEFI Shell interface.
```

After boot, select `View->serial0`, it's already in UEFI Shell.

By checking content of `QEMU_EFI.fd`, it contains two UEFI Applications (`Shell` and `UiApp`). how to enter `UiApp`? 如果把 `UiApp.efi`拷贝到`hda-content/`目录, 在Shell中执行它，则可以进入`UiApp`界面。但是上下键不好使。在Shell中执行`exit`也可以进入`UiApp`.
如果在命令行加上 `-nographic`, 则启动以后当前term直接变成UEFI Shell界面，上下键可以使用。要关掉进程可以通过 `kill` 命令 (term需要`reset`)。

和在Pi4B上一样，Shell下执行`vmlinux initrd=initrd`可以启动到`initramfs`.

### Install from ISO

ref:

- [Qemu cmdline options](https://wiki.gentoo.org/wiki/QEMU/Options)
- [How to launch ARM aarch64 VM with QEMU from scratch](https://futurewei-cloud.github.io/ARM-Datacenter/qemu/how-to-launch-aarch64-vm/)
- [为QEMU创建基于UEFI的AARCH64虚拟机](https://blog.csdn.net/fastboy_abc/article/details/86635638)
- [ARM64 Ubuntu cloud image on Qemu](https://wiki.ubuntu.com/ARM64/QEMU)
- [ARM64 Ubuntu cloud image on Win10](https://gist.github.com/billti/d904fd6124bf6f10ba2c1e3736f0f0f7)
- [qemu documentation](https://qemu.readthedocs.io/_/downloads/en/stable/pdf/)

按照 [How to launch ARM aarch64 VM with QEMU from scratch](https://futurewei-cloud.github.io/ARM-Datacenter/qemu/how-to-launch-aarch64-vm/) 进行安装。

storages:

1. ROM for `guest firmware`: `ROM firmware image can be loaded with -pflash`. The static one is read-only.

    > Now you'll need to create pflash volumes for UEFI. Two volumes are required, one static one for the UEFI firmware, and another dynamic one to store variables. Both need to be exactly 64M in size.
    >
    > --- [ARM64 Ubuntu cloud image on Qemu](https://wiki.ubuntu.com/ARM64/QEMU)

    ```
    dd if=/dev/zero of=flash0.img bs=1M count=64
    dd if=/dev/zero of=flash1.img bs=1M count=64
    dd if=QEMU_EFI.fd of=flash0.img conv=notrunc
    ```
    > OVMF is a TianoCore project to enable UEFI support for Virtual Machines. OVMF contains a sample UEFI firmware and a separate non-volatile variable store for QEMU.
    >
    > It is advised to make a local copy of the non-volatile variable store `OVMF_VARS.fd` for your virtual machine.
    >
    > --- https://wiki.archlinux.org/title/Unified_Extensible_Firmware_Interface#OVMF_for_virtual_machines

2. hdd for iso (readonly):
    - `-drive file=ubuntu-image.img,if=none,id=drive0,cache=writeback -device virtio-blk,drive=drive0,bootindex=0`
3. hdd for guest (read-write):
    - `qemu-img create ubuntu-image.img 10G`
    - `-drive file=/home/bruin/distro/mini.iso,if=none,id=drive1,cache=writeback -device virtio-blk,drive=drive1,bootindex=1`
4. network: `-netdev user,id=vnet,hostfwd=:127.0.0.1:0-:22 -device virtio-net-pci,netdev=vnet`
    - ssh from host to guest: https://patchwork.kernel.org/project/qemu-devel/patch/20170225213158.32452-1-vincent@bernat.im/
    - `127.0.0.1:0` means dynamically allocate a port on host. to check the allocated port, use `ss -antp|grep LISTEN`; then `ssh localhost -p <port>`.

```
$ qemu-system-aarch64 \
    -M virt \
    -cpu cortex-a72 \
    -smp 4 \
    -m 1024 \
    -nographic \
    -netdev user,id=vnet,hostfwd=:127.0.0.1:0-:22 -device virtio-net-pci,netdev=vnet \
    -drive file=ubuntu-image.img,if=none,id=drive0,cache=writeback -device virtio-blk,drive=drive0,bootindex=0 \
    -drive file=/home/bruin/distro/mini.iso,if=none,id=drive1,cache=writeback -device virtio-blk,drive=drive1,bootindex=1 \
    -drive file=flash0.img,format=raw,if=pflash \
    -drive file=flash1.img,format=raw,if=pflash

...
   +---------------- [!!] Finish the installation -------------------------+
   │                                                                       |
   │                         Installation complete                         │
   │ Installation is complete, so it is time to boot into your new system. │
   │ Make sure to remove the installation media (CD-ROM, floppies), so     │
   │ that you boot into the new system rather than restarting the          │
   │ installation.                                                         │
   │                                                                       │
   │     <Go Back>                                          <Continue>     │
   +-----------------------------------------------------------------------+
```

Quit Qemu by killing the process. At this point, the `flash1.img` has already been updated:

```
$ xxd flash1.img
00000000: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000010: 8d2b f1ff 9676 8b4c a985 2747 075b 4f50  .+...v.L..'G.[OP
00000020: 0000 0c00 0000 0000 5f46 5648 360e 0000  ........_FVH6...
00000030: 4800 f8f8 0000 0002 0001 0000 0000 0400  H...............
00000040: 0000 0000 0000 0000 782c f3aa 7b94 9a43  ........x,..{..C
00000050: a180 2e14 4ec3 7792 b8ff 0300 5afe 0000  ....N.w.....Z...
00000060: 0000 0000 aa55 3f00 0700 0000 0000 0000  .....U?.........
00000070: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000080: 0000 0000 0000 0000 0800 0000 0400 0000  ................
00000090: 1140 70eb 0214 d311 8e77 00a0 c969 723b  .@p......w...ir;
000000a0: 4d00 5400 4300 0000 0100 0000 aa55 3c00  M.T.C........U<.
000000b0: 0300 0000 0000 0000 0000 0000 0000 0000  ................
000000c0: 0000 0000 0000 0000 0000 0000 0000 0000  ................
000000d0: 2800 0000 0100 0000 16d6 474b d6a8 5245  (.........GK..RE
000000e0: 9d44 ccad 2e0f 4cf9 4900 6e00 6900 7400  .D....L.I.n.i.t.
000000f0: 6900 6100 6c00 4100 7400 7400 6500 6d00  i.a.l.A.t.t.e.m.
00000100: 7000 7400 4f00 7200 6400 6500 7200 0000  p.t.O.r.d.e.r...
00000110: 01ff ffff aa55 3f00 0300 0000 0000 0000  .....U?.........
00000120: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000130: 0000 0000 0000 0000 1400 0000 1904 0000  ................
00000140: 4549 3259 44ec 0d4c b1cd 9db1 39df 070c  EI2YD..L....9...
00000150: 4100 7400 7400 6500 6d00 7000 7400 2000  A.t.t.e.m.p.t. .
00000160: 3100 0000 0000 0000 0000 0000 0000 0000  1...............
00000170: 0000 0000 0001 0000 0000 0000 0000 4174  ..............At
00000180: 7465 6d70 7420 3100 0000 0000 0000 0000  tempt 1.........
00000190: 0000 0000 0000 0000 0000 0000 0000 0000  ................
...
```

Boot the installed system using the following command (i.e., removing the iso image):

```
$ qemu-system-aarch64 \
    -M virt \
    -cpu cortex-a72 \
    -smp 4 \
    -m 1024 \
    -nographic \
    -netdev user,id=vnet,hostfwd=:127.0.0.1:0-:22 -device virtio-net-pci,netdev=vnet \
    -drive file=ubuntu-image.img,if=none,id=drive0,cache=writeback -device virtio-blk,drive=drive0,bootindex=0 \
    -drive file=flash0.img,format=raw,if=pflash,readonly=on \
    -drive file=flash1.img,format=raw,if=pflash
...
FSOpen: Open '\EFI\ubuntu\grubaa64.efi' Success
[Bds] Expand HD(1,GPT,0377D22E-35DF-4BD3-A3A4-49D39F0CFCDF,0x800,0x100000)/\EFI\ubunt
u\grubaa64.efi -> PciRoot(0x0)/Pci(0x2,0x0)/HD(1,GPT,0377D22E-35DF-4BD3-A3A4-49D39F0C
FCDF,0x800,0x100000)/\EFI\ubuntu\grubaa64.efi
SetBootOrderFromQemu: setting BootOrder: success
[Bds]OsIndication: 0000000000000000
[Bds]=============Begin Load Options Dumping ...=============
  Driver Options:
  SysPrep Options:
  Boot Options:
    Boot0005: ubuntu             0x0001
    Boot0002: UEFI Misc Device 2                 0x0001
    Boot0000: UiApp              0x0109
    Boot0001: UEFI Misc Device           0x0001
    Boot0004: EFI Internal Shell                 0x0001
  PlatformRecovery Options:
    PlatformRecovery0000: Default PlatformRecovery               0x0001
[Bds]=============End Load Options Dumping=============
[Bds]BdsWait ...Zzzzzzzzzzzz...
[Bds]BdsWait(3)..Zzzz...
[Bds]BdsWait(2)..Zzzz...
[Bds]BdsWait(1)..Zzzz...
[Bds]Exit the waiting!
[Bds]Stop Hotkey Service!
[Bds]UnregisterKeyNotify: 000C/0000 Success
[Bds]UnregisterKeyNotify: 0017/0000 Success
[Bds]UnregisterKeyNotify: 0000/000D Success
Memory  Previous  Current    Next
 Type    Pages     Pages     Pages
======  ========  ========  ========
  09    00000000  00000010  00000014
  0A    00000000  00000020  00000028
  00    00000000  00000000  00000000
  06    0000012C  00000280  00000320
  05    00000096  00000250  000002E4
  03    000003E8  0000034C  000003E8
  04    00002EE0  00002508  00002EE0
  01    00000014  00000000  00000014
  02    00000000  00000000  00000000
Memory Type Information settings change.
[Bds]Booting ubuntu
FSOpen: Open '\EFI\ubuntu\grubaa64.efi' Success
[Bds] Expand HD(1,GPT,0377D22E-35DF-4BD3-A3A4-49D39F0CFCDF,0x800,0x100000)/\EFI\ubunt
u\grubaa64.efi -> PciRoot(0x0)/Pci(0x2,0x0)/HD(1,GPT,0377D22E-35DF-4BD3-A3A4-49D39F0C
FCDF,0x800,0x100000)/\EFI\ubuntu\grubaa64.efi
BdsDxe: loading Boot0005 "ubuntu" from HD(1,GPT,0377D22E-35DF-4BD3-A3A4-49D39F0CFCDF,
0x800,0x100000)/\EFI\ubuntu\grubaa64.efi
[Security] 3rd party image[0] can be loaded after EndOfDxe: PciRoot(0x0)/Pci(0x2,0x0)
/HD(1,GPT,0377D22E-35DF-4BD3-A3A4-49D39F0CFCDF,0x800,0x100000)/\EFI\ubuntu\grubaa64.e
fi.
InstallProtocolInterface: 5B1B31A1-9562-11D2-8E3F-00A0C969723B 7E63F040
Loading driver at 0x0007BDF7000 EntryPoint=0x0007BDF8000
Loading driver at 0x0007BDF7000 EntryPoint=0x0007BDF8000
InstallProtocolInterface: BC62157E-3E33-4FEC-9920-2D3B36D750DF 7CEE8898
ProtectUefiImageCommon - 0x7E63F040
  - 0x000000007BDF7000 - 0x00000000001C9000
...
[    4.965572] Couldn't get size: 0x800000000000000e
[    4.966146] MODSIGN: Couldn't get UEFI db list
[    4.967236] Couldn't get size: 0x800000000000000e
[    4.967452] Couldn't get size: 0x800000000000000e
/dev/vda2: recovering journal
/dev/vda2: clean, 72805/622592 files, 618039/2489856 blocks
-.mount
systemd-remount-fs.service
...

Ubuntu 18.04.6 LTS a72 ttyAMA0

a72 login: bruin
Password:
Welcome to Ubuntu 18.04.6 LTS (GNU/Linux 4.15.0-161-generic aarch64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Thu Oct 28 14:36:12 CST 2021

  System load:  1.92              Processes:             108
  Usage of /:   23.2% of 9.29GB   Users logged in:       0
  Memory usage: 11%               IP address for enp0s1: 10.0.2.15
  Swap usage:   0%

0 updates can be applied immediately.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.
bruin@a72:~$ uname -a
Linux a72 4.15.0-161-generic #169-Ubuntu SMP Fri Oct 15 13:41:12 UTC 2021 aarch64 aarch64 aarch64 GNU/Linux
bruin@a72:~$ cat /proc/cmdline
BOOT_IMAGE=/boot/vmlinuz-4.15.0-161-generic root=UUID=4a41e0cf-a40e-486e-9684-261f49fc68ef ro splash quiet vt.handoff=1
$ lsblk -o name,RM,SIZE,RO,TYPE,MOUNTPOINT,UUID
NAME   RM  SIZE RO TYPE MOUNTPOINT UUID
vda     0   10G  0 disk
├─vda1  0  512M  0 part /boot/efi  C6E3-F503
└─vda2  0  9.5G  0 part /          4a41e0cf-a40e-486e-9684-261f49fc68ef
bruin@a72:~$ sudo tree /boot/efi
/boot/efi
└── EFI
    ├── BOOT
    │   └── BOOTAA64.EFI
    └── ubuntu
        ├── grubaa64.efi
        └── grub.cfg

3 directories, 3 files
$ cat /boot/efi/EFI/ubuntu/grub.cfg
search.fs_uuid 4a41e0cf-a40e-486e-9684-261f49fc68ef root
set prefix=($root)'/boot/grub'
configfile $prefix/grub.cfg
$ grep initrd /boot/grub/grub.cfg
        initrd  /boot/initrd.img-4.15.0-161-generic
                initrd  /boot/initrd.img-4.15.0-161-generic
                initrd  /boot/initrd.img-4.15.0-161-generic
$ sudo poweroff
```

Apparently, the automatically selected bootloader during BDS is `grubaa64.efi` located on ESP partition (under folder `/EFI/ubuntu/`).

### boot into UEFI

How to boot into UEFI Shell? Press `ESC` once see the `[Bds]BdsWait ...` on the console, then boot into Boot Manager, and from Boot Manger, enter the UEFI Shell:

```
...
[Bds]=============End Load Options Dumping=============
[Bds]BdsWait ...Zzzzzzzzzzzz...
[Bds]BdsWait(3)..Zzzz...
[Bds]BmHotkeyCallback: 0017:0000
[Bds]Hotkey for Boot0000 pressed - Success
[Bds]Exit the waiting!
[Bds] Booting Boot Manager Menu.
...
/------------------------------------------------------------------------------\
|                                Boot Manager                                  |
\------------------------------------------------------------------------------/

                                                         Device Path :
   Boot Manager Menu                                     Fv(64074AFE-340A-4BE6-
                                                         94BA-91B5B4D0F71E)/FvF
   ubuntu                                                ile(7C04A583-9E3E-4F1C
   UEFI Misc Device 2                                    -AD65-E05268D0B4D1)
   UEFI Misc Device
   EFI Internal Shell
   UEFI PXEv4 (MAC:525400123456)

   Use the <^> and <v> keys to choose a boot option,
   the <Enter> key to select a boot option, and the
   <Esc> key to exit the Boot Manager Menu.

/------------------------------------------------------------------------------\
|                                                                              |
| ^v=Move Highlight       <Enter>=Select Entry      Esc=Exit                   |
\------------------------------------------------------------------------------/

UEFI v2.70 (EDK II, 0x00010000)008-7F9B-4F30-87AC-60C9FEF5DA4E 7BF872F0
Mapping table
      FS0: Alias(s):HD0b:;BLK1:
          PciRoot(0x0)/Pci(0x2,0x0)/HD(1,GPT,0377D22E-35DF-4BD3-A3A4-49D39F0CFCDF,0x800,0x100000)
     BLK3: Alias(s):
          VenHw(93E34C7E-B50E-11DF-9223-2443DFD72085,00)
     BLK0: Alias(s):
          PciRoot(0x0)/Pci(0x2,0x0)
     BLK2: Alias(s):
          PciRoot(0x0)/Pci(0x2,0x0)/HD(2,GPT,EB7E1E8E-7750-4B50-9A27-D40B90E51048,0x100800,0x12FF000)

Press ESC in 3 seconds to skip startup.nsh or any other key to continue.
Shell> fs0:
FS0:> cd EFI\ubuntu
FS0:\EFI\ubuntu> dir
10/28/2021  04:33 <DIR>         8,192  .
10/28/2021  04:33 <DIR>         8,192  ..
10/28/2021  04:33                 117  grub.cfg
FS0:\EFI\ubuntu\>           1,873,792  grubaa64.efi
          2 File(s)   1,873,909 bytes
```

- [How grub tells kernel the initrd address?](https://unix.stackexchange.com/questions/58793/how-is-a-linux-kernel-capable-of-accessing-its-assigned-initramfs-initrd)
- [analyzing linux boot process](https://opensource.com/article/18/1/analyzing-linux-boot-process)

> The following is an excerpt from the U-Boot help for bootm command:
>
> ```
> bootm [addr [arg ...]]
>
> - boot application image stored in memory
>    passing arguments 'arg ...'; when booting a Linux kernel,
>    'arg' can be the address of an initrd image
>    When booting a Linux kernel which requires a flat device-tree
>    a third argument is required which is the address of the
>    device-tree blob. To boot that kernel without an initrd image,
>    use a '-' for the second argument. If you do not pass a third
>    a bd_info struct will be passed instead
> ```
>
> --- https://stackoverflow.com/questions/21750145/bootm-without-device-tree-blob

### boot kernel via EFI_STUB

从log观察，device enumeration 没有使用dtb, 用的是ACPI。启动的过程多了一些打印，估计通过 EFI_STUB 启动会触发一些打印开关。

```
root@a72 # cd /boot/efi
root@a72:/boot/efi# zcat ../vmlinuz >vmlinux
root@a72:/boot/efi# cp ../initrd.img .
root@a72:/boot/efi# file vmlinux
vmlinux: MS-DOS executable           <== this suggests that vmlinux is EFI_STUBed
root@a72:/boot/efi# reboot
...
[Bds]=============End Load Options Dumping=============
[Bds]BdsWait ...Zzzzzzzzzzzz...
[Bds]BdsWait(3)..Zzzz...
[Bds]BdsWait(2)..Zzzz...             <== press ESC key
[Bds]BmHotkeyCallback: 0017:0000
[Bds]Hotkey for Boot0000 pressed - Success
[Bds]Exit the waiting!
[Bds] Booting Boot Manager Menu.
...
FS0:\> vmlinux initrd=\initrd.img root=/dev/vda2
[Security] 3rd party image[0] can be loaded after EndOfDxe: PciRoot(0x0)/Pci(0x2,0x0)/HD(1,GPT,0377D22E-35DF-4BD3-A3A4-49D39F0CFCDF,0x800,0x100000)/\vmlinux.
InstallProtocolInterface: 5B1B31A1-9562-11D2-8E3F-00A0C969723B 7CE69040
Loading driver at 0x00078FF9000 EntryPoint=0x00079F6F1E0
Loading driver at 0x00078FF9000 EntryPoint=0x00079F6F1E0
InstallProtocolInterface: BC62157E-3E33-4FEC-9920-2D3B36D750DF 7CE6A398
ProtectUefiImageCommon - 0x7CE69040
  - 0x0000000078FF9000 - 0x00000000017FC000
SetUefiImageMemoryAttributes - 0x0000000078FF9000 - 0x0000000000001000 (0x0000000000004008)
SetUefiImageMemoryAttributes - 0x0000000078FFA000 - 0x0000000001023000 (0x0000000000020008)
SetUefiImageMemoryAttributes - 0x000000007A01D000 - 0x00000000007D8000 (0x0000000000004008)
InstallProtocolInterface: 752F3136-4E16-4FDC-A22A-E5F46812F4CA 7F80BFA8
EFI stub: Booting Linux Kernel...
EFI stub: EFI_RNG_PROTOCOL unavailable, no randomness supplied
EFI stub: Generating empty DTB
FSOpen: Open 'initrd.img' Success       <== so, it's the bootloader who is reponsible for loading initrd into ram
EFI stub: Exiting boot services and installing virtual address map...
SetUefiImageMemoryAttributes - 0x000000007F650000 - 0x0000000000040000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x000000007C2E0000 - 0x0000000000040000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x000000007C290000 - 0x0000000000040000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x000000007C240000 - 0x0000000000040000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x000000007C150000 - 0x0000000000040000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x000000007F610000 - 0x0000000000030000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x000000007C050000 - 0x0000000000030000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x000000007BFC0000 - 0x0000000000030000 (0x0000000000000008)
[    0.000000] Booting Linux on physical CPU 0x0000000000 [0x410fd083]
[    0.000000] Linux version 4.15.0-161-generic (buildd@bos02-arm64-006) (gcc version 7.5.0 (Ubuntu/Linaro 7.5.0-3ubuntu1~18.04)) #169-Ubuntu SMP Fri Oct 15 13:41:12 UTC 2021 (U
buntu 4.15.0-161.169-generic 4.15.18)
[    0.000000] efi: Getting EFI parameters from FDT:
[    0.000000] efi: EFI v2.70 by EDK II
[    0.000000] efi:  SMBIOS 3.0=0x7f6c0000  MEMATTR=0x7ced4018  ACPI 2.0=0x7c040018
[    0.000000] ACPI: Early table checksum verification disabled
[    0.000000] ACPI: RSDP 0x000000007C040018 000024 (v02 BOCHS )
[    0.000000] ACPI: XSDT 0x000000007C04FE98 00004C (v01 BOCHS  BXPCFACP 00000001      01000013)
[    0.000000] ACPI: FACP 0x000000007C04FA98 00010C (v05 BOCHS  BXPCFACP 00000001 BXPC 00000001)
[    0.000000] ACPI: DSDT 0x000000007C047518 00487C (v02 BOCHS  BXPCDSDT 00000001 BXPC 00000001)
[    0.000000] ACPI: APIC 0x000000007C04FC18 00018C (v03 BOCHS  BXPCAPIC 00000001 BXPC 00000001)
[    0.000000] ACPI: GTDT 0x000000007C04E998 000060 (v02 BOCHS  BXPCGTDT 00000001 BXPC 00000001)
[    0.000000] ACPI: MCFG 0x000000007C04FF98 00003C (v01 BOCHS  BXPCMCFG 00000001 BXPC 00000001)
[    0.000000] ACPI: SPCR 0x000000007C04F918 000050 (v02 BOCHS  BXPCSPCR 00000001 BXPC 00000001)
[    0.000000] ACPI: SPCR: console: pl011,mmio,0x9000000,9600
[    0.000000] ACPI: NUMA: Failed to initialise from firmware
[    0.000000] NUMA: Faking a node at [mem 0x0000000040000000-0x000000007fffffff]
[    0.000000] NUMA: NODE_DATA [mem 0x7ffebd00-0x7ffeefff]
...
[    0.000000] Kernel command line: vmlinux initrd=\initrd.img root=/dev/vda2
...
[    6.317435] Freeing unused kernel memory: 5824K
[    6.333644] Checked W+X mappings: passed, no W+X pages found
Loading, please wait...                    <== /init script (in initrd) starts
starting version 237
[   10.561903]  vda: vda1 vda2
[   11.466505] virtio_net virtio0 enp0s1: renamed from eth0
Begin: Loading essential drivers ... [   16.840333] raid6: int64x1  gen()   885 MB/s
...
Begin: Running /scripts/init-premount ... done.
Begin: Mounting root file system ... Begin: Running /scripts/local-top ... done.
Begin: Running /scripts/local-premount ... [   19.246254] Btrfs loaded, crc32c=crc32c-arm64-ce
Scanning for Btrfs filesystems
done.
Begin: Will now check root file system ... fsck from util-linux 2.31.1
[/sbin/fsck.ext4 (1) -- /dev/vda2] fsck.ext4 -a -C0 /dev/vda2
/dev/vda2: clean, 72887/622592 files, 624523/2489856 blocks
done.
[   20.399609] EXT4-fs (vda2): mounted filesystem with ordered data mode. Opts: (null)
done.
Begin: Running /scripts/local-bottom ... done.
Begin: Running /scripts/init-bottom ... done.
[   23.660372] random: fast init done
[   24.078479] ip_tables: (C) 2000-2006 Netfilter Core Team
[   24.433793] random: systemd: uninitialized urandom read (16 bytes read)
[   24.453213] systemd[1]: systemd 237 running in system mode. (+PAM +AUDIT +SELINUX +IMA +APPARMOR +SMACK +SYSVINIT +UTMP +LIBCRYPTSETUP +GCRYPT +GNUTLS +ACL +XZ +LZ4 +SECCOMP
+BLKID +ELFUTILS +KMOD -IDN2 +IDN -PCRE2 default-hierarchy=hybrid)
[   24.455631] systemd[1]: Detected virtualization qemu.
[   24.456659] systemd[1]: Detected architecture arm64.
[   24.460560] random: systemd: uninitialized urandom read (16 bytes read)
[   24.461580] random: systemd: uninitialized urandom read (16 bytes read)

Welcome to Ubuntu 18.04.6 LTS!
...
a72 login: bruin
Password:
...
bruin@a72:~$ cat /proc/cmdline
vmlinux initrd=\initrd.img root=/dev/vda2
```

### reinstall using ubuntu 21.10 (kernel 5.13)

Rationale: the previous ubuntu iso is using kernel 4.15, the EFI stuff is too far away from kernel 5.14. So choose newer ubuntu releases:

- r5.4.0-18: [ubuntu server 20.04 ARM64 live CD](http://mirrors.ustc.edu.cn/ubuntu-cdimage/releases/20.04.3/release/ubuntu-20.04.3-live-server-arm64.iso): install ok (using lvm for root)
    - disable `cloud-init`: `systemctl disable cloud-init-local cloud-init cloud-config cloud-final; systemctl stop cloud-init-local cloud-init cloud-config cloud-final`.
- r5.11.0-16: [ubuntu server 21.04 ARM64 live CD](http://mirrors.ustc.edu.cn/ubuntu-cdimage/releases/21.04/release/ubuntu-21.04-live-server-arm64.iso): install ok (online updated installer; not using lvm)
- r5.13.0-19: [ubuntu server 21.10 ARM64 live CD](http://mirrors.ustc.edu.cn/ubuntu-cdimage/releases/21.10/release/ubuntu-21.10-live-server-arm64.iso): install failed.

Where are to-be-installed kernel image in iso?

- `/casper/vmlinuz` ?
- `pool/main/l/linux-signed/linux-image-5.13.0-19-generic_5.13.0-19.19_arm64.deb`?

用 `dpkg-deb -x` 解压 deb 文件以后得到的 kernel 文件和 `casper/vmlinuz` 相同.

What if only replace the kernel for a installed system? 可能 ko 不匹配...

- 使用ubuntu20.04.3安装qemu成功. 缺省使用了lvm, `root=/dev/mapper/ubuntu--vg-ubuntu--lv ro`.
- 先确认在虚拟机上直接用`vmlinux`作为bootloader可以工作:
    - boot into VM
    - cp and zcat vmlinuz from `/boot/` to `/boot/efi`, the latter is the ESP partition.
    - cp initrg.img from `/boot/` to `/boot/efi`.
    - get `root=` cmdline from `/proc/cmdline`: `root=/dev/mapper/ubuntu--vg-ubuntu--lv ro`
    - reboot into UEFI Shell, do `vmlinux initrd=\initrd.img root=/dev/mapper/ubuntu--vg-ubuntu--lv ro`. Linux boot correctly.
- 从`ubuntu21.04`以及`ubunt21.10`镜像中得到 `vmlinux.5.11`, `vmlinux.5.13`并 scp 到 `/boot/efi/`: `scp -P <port> <file> localhost:/boot/efi`
- boot into UEFI shell, 用vmlinux.5.11启动(`initrd`不变), 报`/dev/mapper/ubuntu--vg-ubuntu--lv does not exist`, drop into `(initramfs)`.
- according to [debian initrd](https://wiki.debian.org/Initrd), it seems that `initrd.img` is created dynamically after installation.


- [gdb: using separate symbol files][https://medium.com/@ffugavr/creating-and-using-debug-symbol-tables-with-cmake-and-gdb-7554868d51ea]
- [--add-gnu-debuglink](https://stackoverflow.com/questions/44028934/how-to-use-add-gnu-debuglink-to-keep-gdb-symbol-files-in-a-mounted-folder)


### backto Pi4: use initrd/vmlinux and rootfs on Pi4B

Why go back to Pi4B?

- check whether or not the same initrd/vmlinux and rootfs for Qemu can boot on Pi4B.
- check what if provide dtb from cmdline: we only have dtb for Pi4B, not for the Qemu VM.

Do the following:

- copy `initrd.img` and `vmlinux` to `ESP` partition on USB, keep the other files (`config.txt`, `start4.elf`, `RPI_EFI.fd`, etc).
- create a 2nd partition on USB stick, `mkfs.ext4`, and then copy rootfs to it (using `tar`)
- modify `/etc/fstab`: use `/dev/sda1` and `/dev/sda2` for `/boot/efi` and `/` mount points.

2021.11.8: redo the steps for ubuntu 21.04 (kernel `r5.11.0-38`).

#### not use `dtb=`

Then it can sucessfully boot into Linux (w/o network):

```
FS0:\> vmlinux initrd=\initrd.img root=/dev/sda2
[Security] 3rd party image[0] can be loaded after EndOfDxe: PcieRoot(0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/USB(0x0,0x0)/USB(0x0,0x0)/HD(1,MBR,0x04EA7D7A,0x800,0x100000)/\vmlinux.
InstallProtocolInterface: 5B1B31A1-9562-11D2-8E3F-00A0C969723B 35833040
Loading driver at 0x00031BA4000 EntryPoint=0x00032B1A1E0
Loading driver at 0x00031BA4000 EntryPoint=0x00032B1A1E0
Variable store not found?
InstallProtocolInterface: BC62157E-3E33-4FEC-9920-2D3B36D750DF 35834518
ProtectUefiImageCommon - 0x35833040
  - 0x0000000031BA4000 - 0x00000000017FC000
InstallProtocolInterface: 752F3136-4E16-4FDC-A22A-E5F46812F4CA 3B2FEEF8
EFI stub: Booting Linux Kernel...
EFI stub: Generating empty DTB
FSOpen: Open 'initrd.img' Success
EFI stub: Exiting boot services and installing virtual address map...
XhcClearBiosOwnership: called to clear BIOS ownership
SetUefiImageMemoryAttributes - 0x0000000037160000 - 0x0000000000040000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x0000000033DF0000 - 0x0000000000040000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x0000000033DA0000 - 0x0000000000040000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x0000000037120000 - 0x0000000000030000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x0000000033D30000 - 0x0000000000030000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x0000000033CF0000 - 0x0000000000030000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x0000000033CB0000 - 0x0000000000030000 (0x0000000000000008)
[    0.000000] Booting Linux on physical CPU 0x0000000000 [0x410fd083]
[    0.000000] Linux version 4.15.0-161-generic (buildd@bos02-arm64-006) (gcc version 7.5.0 (Ubuntu/Linaro 7.5.0-3ubuntu1~18.04)) #169-Ubuntu SMP Fri Oct 15 13:41:12 UTC 2021 (Ubuntu 4.15.0-161.169-generic 4.15.18)
[    0.000000] efi: Getting EFI parameters from FDT:
[    0.000000] efi: EFI v2.70 by EDK2
[    0.000000] efi:  ACPI 2.0=0x33d70018  SMBIOS=0x371c0000  SMBIOS 3.0=0x33c90000  MEMATTR=0x3582e018  RNG=0x372dd098
[    0.000000] efi: seeding entropy pool
...
bruin@a72:~$ uname -a
Linux a72 4.15.0-161-generic #169-Ubuntu SMP Fri Oct 15 13:41:12 UTC 2021 aarch64 aarch64 aarch64 GNU/Linux
bruin@a72:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
```

FIXME: what `EFI stub: Generating empty DTB` and `efi: Getting EFI parameters from FDT:` imply?

> CONFIG_EFI_PARAMS_FROM_FDT:
>
> Select this config option from the architecture Kconfig if the EFI runtime support gets system table address, memory map address, and other parameters from the device tree.
>
> --- https://cateee.net/lkddb/web-lkddb/EFI_PARAMS_FROM_FDT.html


#### use `dtb=\bcm2711-rpi-4-b.dtb`

It stalls at begining:

```
FS0:\> vmlinux initrd=\initrd.img root=/dev/sda2 dtb=\bcm2711-rpi-4-b.dtb
[Security] 3rd party image[0] can be loaded after EndOfDxe: PcieRoot(0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/USB(0x0,0x0)/USB(0x0,0x0)/HD(1,MBR,0x04EA7D7A,0x800,0x100000)/\vmlinux.
InstallProtocolInterface: 5B1B31A1-9562-11D2-8E3F-00A0C969723B 35840040
Loading driver at 0x00031BA4000 EntryPoint=0x00032B1A1E0
Loading driver at 0x00031BA4000 EntryPoint=0x00032B1A1E0
Variable store not found?
InstallProtocolInterface: BC62157E-3E33-4FEC-9920-2D3B36D750DF 35840B98
ProtectUefiImageCommon - 0x35840040
  - 0x0000000031BA4000 - 0x00000000017FC000
InstallProtocolInterface: 752F3136-4E16-4FDC-A22A-E5F46812F4CA 3B2FEEF8
EFI stub: Booting Linux Kernel...
FSOpen: Open 'bcm2711-rpi-4-b.dtb' Success
EFI stub: Using DTB from command line
FSOpen: Open 'initrd.img' Success
EFI stub: Exiting boot services and installing virtual address map...
XhcClearBiosOwnership: called to clear BIOS ownership
SetUefiImageMemoryAttributes - 0x0000000037160000 - 0x0000000000040000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x0000000033DF0000 - 0x0000000000040000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x0000000033DA0000 - 0x0000000000040000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x0000000037120000 - 0x0000000000030000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x0000000033D30000 - 0x0000000000030000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x0000000033CF0000 - 0x0000000000030000 (0x0000000000000008)
SetUefiImageMemoryAttributes - 0x0000000033CB0000 - 0x0000000000030000 (0x0000000000000008)
```

FIXME:

- how to debug?
- is this related to serial console settings?
    - `console=ttyAMA0,115200n8`?
    - `ACPI: SPCR: console: pl011...`: Serial Port Console Redirection
        - `CONFIG_ACPI`
        - `CONFIG_ARCH_SUPPORTS_ACPI`
        - `CONFIG_ACPI_SPCR_TABLE`
    - EARLYCON:
        - `CONFIG_EFI_EARLYCON`
        - `CONFIG_SERIAL_EARLYCON`
        - [kernel config](https://www.kernelconfig.io/config_acpi?q=&kernelversion=5.11.20&arch=arm64)


2021.11.8: using u2104 (`r5.11.0-38`)

```
FS0:\> vmlinux-5.11.0-38 initrd=\initrd.img-5.11.0-38 root=/dev/sda2 dtb=\bcm271
1-rpi-4-b.dtb
FSOpen: Open '\vmlinux-5.11.0-38' Success
FSOpen: Open '\vmlinux-5.11.0-38' Success
FSOpen: Open '\vmlinux-5.11.0-38' Success
FSOpen: Open '\vmlinux-5.11.0-38' Success
[Security] 3rd party image[0] can be loaded after EndOfDxe: PcieRoot(0x0)/Pci(0x0,0x0)/Pci(0x0,0x0)/USB(0x0,0x0)/USB(0x0,0x0)/HD(1,MBR,0x04EA7D7A,0x800,0x100000)/\vmlinux-5.11.0-38.
InstallProtocolInterface: 5B1B31A1-9562-11D2-8E3F-00A0C969723B 35827040
Loading driver at 0x0002E550000 EntryPoint=0x0003014C2F8
Loading driver at 0x0002E550000 EntryPoint=0x0003014C2F8
Variable store not found?
InstallProtocolInterface: BC62157E-3E33-4FEC-9920-2D3B36D750DF 3583BA18
ProtectUefiImageCommon - 0x35827040
  - 0x000000002E550000 - 0x00000000027C0000
InstallProtocolInterface: 752F3136-4E16-4FDC-A22A-E5F46812F4CA 3B2FEEF8
EFI stub: Booting Linux Kernel...
EFI stub: ERROR: Ignoring DTB from command line.         <== 这一行和 r4.15 不同
EFI stub: Generating empty DTB
FSOpen: Open 'initrd.img-5.11.0-38' Success
EFI stub: Loaded initrd from command line option
EFI stub: Exiting boot services and installing virtual address map..
...
Last login: Mon Nov  8 01:22:36 UTC 2021 on ttyAMA0
bruin@u2104:~$ uname -a
Linux u2104 5.11.0-38-generic #42-Ubuntu SMP Fri Sep 24 13:11:27 UTC 2021 aarch64 aarch64 aarch64 GNU/Linux
bruin@u2104:~$ cat /proc/cmdline
vmlinux-5.11.0-38 initrd=\initrd.img-5.11.0-38 root=/dev/sda2 dtb=\bcm2711-rpi-4-b.dtb
bruin@u2104:~$ ls -la /sys/firmware/devicetree
total 0
drwxr-xr-x 2 root root 0 Nov  8 01:42 .
drwxr-xr-x 6 root root 0 Oct 21 02:37 ..
```

The reason `EFI stub: ERROR: Ignoring DTB from command line.` is in the [efi_pe_entry()](https://elixir.bootlin.com/linux/v5.14.17/source/drivers/firmware/efi/libstub/efi-stub.c#L218).

According to <https://elixir.bootlin.com/linux/v5.14.17/source/drivers/firmware/efi/libstub/fdt.c#L226>, it seems that in EFI_STUB:

- an emtpy fdt is created
- the following info are added into fdt:
    - bootargs (cmdline)
    - initrd addr/size
    - EFI table info
    - memory map (updated according to UEFI)

Linux boot: how to tell the kernel use fdt or uefi-runtime-tables to config drivers?



##### howto turn on JTAG

UEFI setting: Boot Manager -> Device Manager -> Raspberry Pi Config -> Debugging Config -> JTAG routing -> Enable JTAG via GPIO.

The problem: change and F10 (save), then reboot, the change does not saved.

> You can usually find platform specific options that are exposed as PCDs in the .dsc for the platform, along with their default value.
>
> Then, if you want to override an option, you can just add --pcd <full_name_of_PCD>=<override_value> when invoking build.
>
> --- https://github.com/pftf/RPi4/issues/175

build with `--pcd gRaspberryPiTokenSpaceGuid.PcdDebugEnableJTAG=1`.

How to dump `.FD` varaibles:

- https://toscode.gitee.com/mirrors_hlandau/ovmfvartool: not working with `RPI_EFI.fd`, or stripped one (remove bl31 at begining).
- http://smackerelofopinion.blogspot.com/2011/05/dumping-uefi-variables.html: use `# dhclient -4` to get an IP first, then `# apt install fwts`.

    ```
    root@u2104:/etc# fwts uefidump -
    Results generated by fwts: Version V21.03.00 (2021-03-29 08:56:51).

    Some of this work - Copyright (c) 1999 - 2021, Intel Corp. All rights reserved.
    Some of this work - Copyright (c) 2010 - 2021, Canonical.
    Some of this work - Copyright (c) 2016 - 2021, IBM.
    Some of this work - Copyright (c) 2017 - 2021, ARM Ltd.

    This test run on 09/11/21 at 07:32:43 on host Linux u2104 5.11.0-38-generic
    #42-Ubuntu SMP Fri Sep 24 13:11:27 UTC 2021 aarch64.

    Command: "fwts uefidump -".
    Running tests: uefidump.

    uefidump: Dump UEFI variables.
    --------------------------------------------------------------------------------
    Test 1 of 1: Dump UEFI Variables.
    Name: AssetTag
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 66 bytes of data
      Data: 0000: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
      Data: 0010: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
      Data: 0020: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
      Data: 0030: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
      Data: 0040: 00 00                                            ..

    Name: Boot0000
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Active: Yes
      Info: UiApp
      Path: \FV(9a15aa37-d555-4a4e-b5-41-86-39-1f-f6-81-64)\FVFILE(462caa21-7614-4503-83-6e-8a-b6-f4-66-23-31)

    Name: Boot0001
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Active: Yes
      Info: SD/MMC on Arasan SDHCI
      Path: \VENDOR(100c2cfa-b586-4198-9b4c-1683d195b1da)
      OptionalData:
      Data: 0000: 4E AC 08 81 11 9F 59 4D 85 0E E2 1A 52 2C 59 B2  N.....YM....R,Y.

    Name: Boot0002
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Active: Yes
      Info: UEFI SanDisk Cruzer Fit 4C530202800309122232
      Path: \ACPI(0xa0841d0,0x0)\PCI(0x0,0x0)\PCI(0x0,0x0)\USB(0x0,0x0)\USB(0x0,0x0)
      OptionalData:
      Data: 0000: 4E AC 08 81 11 9F 59 4D 85 0E E2 1A 52 2C 59 B2  N.....YM....R,Y.

    Name: Boot0003
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Active: Yes
      Info: UEFI PXEv4 (MAC:E45F0148F30D)
      Path: \MACADDR(e4:5f:1:48:f3:d,0x1)\IPv4(0.0.0.0,0.0.0.0,0,0,0,0,0.0.0.0,0.0.0.0)
      OptionalData:
      Data: 0000: 4E AC 08 81 11 9F 59 4D 85 0E E2 1A 52 2C 59 B2  N.....YM....R,Y.

    Name: Boot0004
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Active: Yes
      Info: UEFI PXEv6 (MAC:E45F0148F30D)
      Path: \MACADDR(e4:5f:1:48:f3:d,0x1)\IPv6(0:0:0:0:0:0:0:0,0:0:0:0:0:0:0:0,0,0,0,0,64,0:0:0:0:0:0:0:0)
      OptionalData:
      Data: 0000: 4E AC 08 81 11 9F 59 4D 85 0E E2 1A 52 2C 59 B2  N.....YM....R,Y.

    Name: Boot0005
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Active: Yes
      Info: UEFI HTTPv4 (MAC:E45F0148F30D)
      Path: \MACADDR(e4:5f:1:48:f3:d,0x1)\IPv4(0.0.0.0,0.0.0.0,0,0,0,0,0.0.0.0,0.0.0.0)
      OptionalData:
      Data: 0000: 4E AC 08 81 11 9F 59 4D 85 0E E2 1A 52 2C 59 B2  N.....YM....R,Y.

    Name: Boot0006
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Active: Yes
      Info: UEFI HTTPv6 (MAC:E45F0148F30D)
      Path: \MACADDR(e4:5f:1:48:f3:d,0x1)\IPv6(0:0:0:0:0:0:0:0,0:0:0:0:0:0:0:0,0,0,0,0,64,0:0:0:0:0:0:0:0)
      OptionalData:
      Data: 0000: 4E AC 08 81 11 9F 59 4D 85 0E E2 1A 52 2C 59 B2  N.....YM....R,Y.

    Name: Boot0007
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Active: No
      Info: UEFI Shell
      Path: \FV(9a15aa37-d555-4a4e-b5-41-86-39-1f-f6-81-64)\FVFILE(7c04a583-9e3e-4f1c-ad-65-e0-52-68-d0-b4-d1)

    Name: BootCurrent
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x6 (BootServ,RunTime)
      BootCurrent: 0x0007

    Name: BootDiscoveryPolicy
      GUID: 5B6F7107-BB3C-4660-92CD-542690280BBD
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: 02 00 00 00                                      ....

    Name: BootOptionSupport
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x6 (BootServ,RunTime)
      BootOptionSupport: 0x0313

    Name: BootOrder
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Boot Order: 0x0000,0x0002,0x0003,0x0004,0x0005,0x0006,0x0007,0x0001

    Name: ConIn
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Device Path: \USBCLASS(0xffff,0xffff,0x3,0x1,0x1)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(UnknownGUID 7d916d80-5bb1-458c-a4-8f-e2-5f-dd-51-ef-94)

    Name: ConInDev
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x6 (BootServ,RunTime)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(PC-ANSI)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(VT-100)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(VT-100+)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(VT-UTF8)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(UnknownGUID 7d916d80-5bb1-458c-a4-8f-e2-5f-dd-51-ef-94)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(UnknownGUID e4364a7f-f825-430e-9d-3a-9c-9b-e6-81-7c-a5)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(UnknownGUID fbfca56b-bb36-4b78-aa-ab-be-1b-97-ec-7c-cb)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(UnknownGUID 8e46dddd-3d49-4a9d-b8-75-3c-08-6f-6a-a2-bd)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(UnknownGUID fc7dd6e0-813c-434d-b4-da-3b-d6-49-e9-e1-5a)

    Name: ConOut
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(UnknownGUID 7d916d80-5bb1-458c-a4-8f-e2-5f-dd-51-ef-94)

    Name: ConOutDev
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x6 (BootServ,RunTime)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(PC-ANSI)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(VT-100)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(VT-100+)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(VT-UTF8)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(UnknownGUID 7d916d80-5bb1-458c-a4-8f-e2-5f-dd-51-ef-94)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(UnknownGUID e4364a7f-f825-430e-9d-3a-9c-9b-e6-81-7c-a5)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(UnknownGUID fbfca56b-bb36-4b78-aa-ab-be-1b-97-ec-7c-cb)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(UnknownGUID 8e46dddd-3d49-4a9d-b8-75-3c-08-6f-6a-a2-bd)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(UnknownGUID fc7dd6e0-813c-434d-b4-da-3b-d6-49-e9-e1-5a)

    Name: CpuClock
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: 01 00 00 00                                      ....

    Name: CustomCpuClock
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: DC 05 00 00                                      ....

    Name: DebugEnableJTAG
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: 01 00 00 00                                      ....

    Name: DisplayEnableSShot
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: 01 00 00 00                                      ....

    Name: DisplayEnableScaledVModes
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 1 bytes of data
      Data: 0000: 20

    Name: ErrOut
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(UnknownGUID 7d916d80-5bb1-458c-a4-8f-e2-5f-dd-51-ef-94)

    Name: ErrOutDev
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x6 (BootServ,RunTime)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(PC-ANSI)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(VT-100)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(VT-100+)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(VT-UTF8)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(UnknownGUID 7d916d80-5bb1-458c-a4-8f-e2-5f-dd-51-ef-94)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(UnknownGUID e4364a7f-f825-430e-9d-3a-9c-9b-e6-81-7c-a5)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(UnknownGUID fbfca56b-bb36-4b78-aa-ab-be-1b-97-ec-7c-cb)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(UnknownGUID 8e46dddd-3d49-4a9d-b8-75-3c-08-6f-6a-a2-bd)
      Device Path: \VENDOR(d3987d4b-971a-435f-8caf-4967eb627241)\UART(115200,8,1,1)\VENDOR(UnknownGUID fc7dd6e0-813c-434d-b4-da-3b-d6-49-e9-e1-5a)

    Name: FanOnGpio
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: 00 00 00 00                                      ....

    Name: FanTemp
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: 3C 00 00 00                                      <...

    Name: Key0000
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      PackedValue: 0x40000000
      BootOptionCrc: 0xb87a9384
      BootOption: 0007
      ScanCode: 0x000b
      UnicodeChar: 0x0000

    Name: Key0001
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      PackedValue: 0x40000000
      BootOptionCrc: 0x7fccbfd7
      BootOption: 0000
      ScanCode: 0x0017
      UnicodeChar: 0x0000

    Name: Lang
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Language: eng

    Name: LangCodes
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x6 (BootServ,RunTime)
      Language Codes: eng,fra,eng,fra

    Name: MTC
      GUID: EB704011-1402-11D3-8E77-00A0C969723B
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: 01 00 00 00                                      ....

    Name: MmcDisableMulti
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: 00 00 00 00                                      ....

    Name: MmcEnableDma
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: 01 00 00 00                                      ....

    Name: MmcForce1Bit
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: 00 00 00 00                                      ....

    Name: MmcForceDefaultSpeed
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: 00 00 00 00                                      ....

    Name: MmcSdDefaultSpeedMHz
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: 19 00 00 00                                      ....

    Name: MmcSdHighSpeedMHz
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: 32 00 00 00                                      2...

    Name: OsIndicationsSupported
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x6 (BootServ,RunTime)
      Value: 0x0000000000000041 (EFI_OS_INDICATIONS_BOOT_TO_FW_UI)

    Name: PlatformLang
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Platform Language: en-US

    Name: PlatformLangCodes
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x6 (BootServ,RunTime)
      Platform Language Codes: en-US

    Name: PlatformRecovery0000
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x6 (BootServ,RunTime)
      Active: Yes
      Info: Default PlatformRecovery
      Path: \FILE('\EFI\BOOT\BOOTAA64.EFI')

    Name: RamLimitTo3GB
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: 00 00 00 00                                      ....

    Name: RamMoreThan3GB
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: 00 00 00 00                                      ....

    Name: RtcDaylight
      GUID: B336F62D-4135-4A55-AE4E-4971BBF0885D
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 1 bytes of data
      Data: 0000: 00                                               .

    Name: RtcEpochSeconds
      GUID: B336F62D-4135-4A55-AE4E-4971BBF0885D
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 8 bytes of data
      Data: 0000: EB 1C 8A 61 00 00 00 00                          ...a....

    Name: RtcTimeZone
      GUID: B336F62D-4135-4A55-AE4E-4971BBF0885D
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 2 bytes of data
      Data: 0000: FF 07                                            ..

    Name: SdIsArasan
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: 00 00 00 00                                      ....

    Name: SystemTableMode
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: 00 00 00 00                                      ....

    Name: Timeout
      GUID: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Timeout: 5 seconds

    Name: VarErrorFlag
      GUID: 04B37FE8-F6AE-480B-BDD5-37D98C5E89AA
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 1 bytes of data
      Data: 0000: FF                                               .

    Name: XhciPci
      GUID: CD7CC258-31DB-22E6-9F22-63B0B8EED6B5
      Attr: 0x7 (NonVolatile,BootServ,RunTime)
      Size: 4 bytes of data
      Data: 0000: 00 00 00 00                                      ....
    ```
- `fs0:\> dmpstore -all -s VarDump.txt`
- how to debug via JTAG?
    - for QEMU, see page 35 of book "UEFI编程实践".
    - for RPI4: [SO question](https://github.com/pftf/RPi4/issues/194)
    - [Debugging Raspberry Pi Linux kernel with JTAG and GDB](https://wiki.aalto.fi/display/EmbeddedLinux/Debugging+Raspberry+Pi+Linux+kernel+with+JTAG+and+GDB)

## FPGA u-boot `run ramboot`

refs:

- [efi-entry.S](https://github.com/torvalds/linux/blob/v4.14/arch/arm64/kernel/efi-entry.S#L32)
- [FDT `chosen` node](https://elixir.bootlin.com/linux/v5.15/source/Documentation/devicetree/bindings/chosen.txt)
    - [`bootargs`](https://stackoverflow.com/a/48814885/2947904)
    - [linux kernel中的cmdline的详细介绍](https://blog.51cto.com/u_15278218/2931122)
- [ATAGS vs FDT](https://coderedirect.com/questions/338668/arm-linux-atags-vs-device-tree)
- [how does the bootloader pass the kernel command line to the kernel?](https://stackoverflow.com/a/64881813/2947904)
- [linux device tree runtime config](https://www.kernel.org/doc/html/latest/devicetree/usage-model.html#runtime-configuration)


2021.11.1: 根据[build/load step](http://21.21.21.100:8090/pages/viewpage.action?spaceKey=MyChip&title=MyChip+software+env+setup), 在FPGA上使用`F_A76A55_TWODDR_0928.bit`得到的log如下. 基本可以确认 uboot通过dtb相关参数传给了kernel.

- u-boot 把 FIT (`.itb`) 中的 kernel, initrd, dtb 分别加载到内存中;
- 根据 `bootargs` 环境变量，u-boot 更新了 dtb 的 `chosen/` 节点下的 `bootargs` 属性
- 根据 initrd 在内存中的位置, u-boot 更新了 dtb 的 `chosen/` 节点下的 `linux,initrd-start` 和 `linux,initrd-end` 属性;
- 跳转到kernel的 `entry_point` 前把 `x0` 设置成 dtb 在内存中的地址.

```
NOTICE:  Booting Trusted Firmware
NOTICE:  BL1: v2.4(debug):f85ea578c
NOTICE:  BL1: Built : 15:21:48, Nov  1 2021
INFO:    BL1: RAM 0x207f0000 - 0x207fe000
INFO:    BL1: cortex_a55: CPU workaround for 1530923 was applied
INFO:    BL1: Loading BL2
INFO:    Fip load from memmap dev
INFO:    Loading image id=1 at address 0x207e0000
INFO:    Image id=1 loaded: 0x207e0000 - 0x207e5429
NOTICE:  BL1: Booting BL2
INFO:    Entry point address = 0x207e0000
INFO:    SPSR = 0x3c5
NOTICE:  BL2: v2.4(debug):f85ea578c
NOTICE:  BL2: Built : 15:21:50, Nov  1 2021
INFO:    BL2: Doing platform setup
INFO:    BL2: Loading image id 3
INFO:    Fip load from memmap dev
INFO:    Loading image id=3 at address 0x100000000
INFO:    Image id=3 loaded: 0x100000000 - 0x100009124
INFO:    BL2: Loading image id 5
INFO:    Fip load from memmap dev
INFO:    Loading image id=5 at address 0x102000000
INFO:    Image id=5 loaded: 0x102000000 - 0x102080255
NOTICE:  BL1: Booting BL31
INFO:    Entry point address = 0x100000000
INFO:    SPSR = 0x3cd
NOTICE:  BL31: v2.4(debug):f85ea578c
NOTICE:  BL31: Built : 15:21:54, Nov  1 2021
INFO:    GICv3 without legacy support detected.
INFO:    ARM GICv3 driver initialized in EL3
INFO:    Maximum SPI INTID supported: 63
INFO:    BL31: Initializing runtime services
INFO:    BL31: cortex_a55: CPU workaround for 1530923 was applied
INFO:    BL31: Preparing for EL3 exit to normal world
INFO:    Entry point address = 0x102000000
INFO:    SPSR = 0x3c5

U-Boot 2021.07-rc2-g30af7a57fe (Nov 01 2021 - 15:19:07 +0800)

CPU:   MyChip
DRAM:  512 MiB
Loading Environment from nowhere... OK
In:    serial
Out:   serial
Err:   serial
Hit any key to stop autoboot:  0
MyCorp # print
arch=arm
baudrate=115200
board=MyChip
board_name=MyChip
bootcmd=run distro_bootcmd
bootdelay=2
consoledev=ttyS0
cpu=armv8
fdtcontroladdr=121edf460
othbootargs=earlycon=uart8250,mmio32,0x20020000 loglevel=10
ramboot=setenv bootargs console=$consoledev,$baudrate $othbootargs;setenv uimage_addr 0x112000000;bootm ${uimage_addr}#config-1
stderr=serial
stdin=serial
stdout=serial
vendor=MyCorp

Environment size: 391/16380 bytes
MyCorp # help bootm
bootm - boot application image from memory

Usage:
bootm [addr [arg ...]]
    - boot application image stored in memory
        passing arguments 'arg ...'; when booting a Linux kernel,
        'arg' can be the address of an initrd image
        When booting a Linux kernel which requires a flat device-tree
        a third argument is required which is the address of the
        device-tree blob. To boot that kernel without an initrd image,
        use a '-' for the second argument. If you do not pass a third
        a bd_info struct will be passed instead

For the new multi component uImage format (FIT) addresses
        must be extended to include component or configuration unit name:
        addr:<subimg_uname> - direct component image specification
        addr#<conf_uname>   - configuration specification
        Use iminfo command to get the list of existing component
        images and configurations.

Sub-commands to do part of the bootm sequence.  The sub-commands must be
issued in the order below (it's ok to not issue all sub-commands):
        start [addr [arg ...]]
        loados  - load OS image
        ramdisk - relocate initrd, set env initrd_start/initrd_end
        fdt     - relocate flat device tree
        cmdline - OS specific command line processing/setup
        bdt     - OS specific bd_info processing
        prep    - OS specific prep before relocation or go
        go      - start OS
MyCorp # run ramboot
## Loading kernel from FIT Image at 112000000 ...
   Using 'config-1' configuration
   Verifying Hash Integrity ... OK
   Trying 'kernel-1' kernel subimage
     Description:  MyCorp kernel
     Created:      2021-11-01   7:21:58 UTC
     Type:         Kernel Image
     Compression:  uncompressed
     Data Start:   0x1120000d8
     Data Size:    8552960 Bytes = 8.2 MiB
     Architecture: AArch64
     OS:           Linux
     Load Address: 0x103000000
     Entry Point:  0x103000000
     Hash algo:    sha1
     Hash value:   09c1d4df37b849297731250ef158a9f409d945ff
   Verifying Hash Integrity ... sha1+ OK
## Loading ramdisk from FIT Image at 112000000 ...
   Using 'config-1' configuration
   Verifying Hash Integrity ... OK
   Trying 'ramdisk-1' ramdisk subimage
     Description:  MyCorp ramdisk
     Created:      2021-11-01   7:21:58 UTC
     Type:         RAMDisk Image
     Compression:  uncompressed
     Data Start:   0x1128283d0
     Data Size:    3622912 Bytes = 3.5 MiB
     Architecture: AArch64
     OS:           Linux
     Load Address: 0x00000000
     Entry Point:  0x00000000
     Hash algo:    sha1
     Hash value:   a749f53a3eabf7e1dd65533305696a7c2ec685b3
   Verifying Hash Integrity ... sha1+ OK
## Loading fdt from FIT Image at 112000000 ...
   Using 'config-1' configuration
   Verifying Hash Integrity ... OK
   Trying 'fdt-1' fdt subimage
     Description:  MyCorp device tree
     Created:      2021-11-01   7:21:58 UTC
     Type:         Flat Device Tree
     Compression:  uncompressed
     Data Start:   0x112b9ccc0
     Data Size:    1604 Bytes = 1.6 KiB
     Architecture: AArch64
     Hash algo:    sha1
     Hash value:   339d49bf501c47751aaca0d3e56f2a3c67a7c4f5
   Verifying Hash Integrity ... sha1+ OK
   Booting using the fdt blob at 0x112b9ccc0
   Loading Kernel Image
   Loading Ramdisk to 121b69000, end 121edd800 ... OK
   Loading Device Tree to 0000000121b65000, end 0000000121b68643 ... OK

Starting kernel ...

[    0.000000] Booting Linux on physical CPU 0x0000000000 [0x412fd050]
[    0.000000] Linux version 5.14.0-MyCorpv1.1.0-00001-g15888558210e (bruin@u2004) (aarch64-none-elf-gcc (GNU Toolchain for the A-profile Architecture 10.2-2020.11 (arm-10.16)) 10.2.1 20201103, GNU ld (GNU Toolchain for the A-profile Architecture 10.2-2020.11 (arm-10.16)) 2.35.1.20201028) #1 SMP Mon Nov 1 13:29:06 CST 2021
[    0.000000] Machine model: MyCorp MyChip chiplet Family
[    0.000000] earlycon: uart8250 at MMIO32 0x0000000020020000 (options '')
[    0.000000] printk: bootconsole [uart8250] enabled
[    0.000000] efi: UEFI not found.
[    0.000000] Zone ranges:
[    0.000000]   DMA      [mem 0x0000000102000000-0x0000000181ffffff]
[    0.000000]   DMA32    empty
[    0.000000]   Normal   empty
[    0.000000] Movable zone start for each node
[    0.000000] Early memory node ranges
[    0.000000]   node   0: [mem 0x0000000102000000-0x0000000181ffffff]
[    0.000000] Initmem setup node 0 [mem 0x0000000102000000-0x0000000181ffffff]
[    0.000000] psci: probing for conduit method from DT.
[    0.000000] psci: PSCIv1.1 detected in firmware.
[    0.000000] psci: Using standard PSCI v0.2 function IDs
[    0.000000] psci: MIGRATE_INFO_TYPE not supported.
[    0.000000] psci: SMC Calling Convention v1.2
[    0.000000] percpu: Embedded 29 pages/cpu s79816 r8192 d30776 u118784
[    0.000000] pcpu-alloc: s79816 r8192 d30776 u118784 alloc=29*4096
[    0.000000] pcpu-alloc: [0] 0 [0] 1
[    0.000000] Detected VIPT I-cache on CPU0
[    0.000000] CPU features: detected: GIC system register CPU interface
[    0.000000] CPU features: detected: ARM errata 1165522, 1319367, or 1530923
[    0.000000] Built 1 zonelists, mobility grouping on.  Total pages: 516096
[    0.000000] Kernel command line: console=ttyS0,115200 earlycon=uart8250,mmio32,0x20020000 loglevel=10
[    0.000000] Dentry cache hash table entries: 262144 (order: 9, 2097152 bytes, linear)
[    0.000000] Inode-cache hash table entries: 131072 (order: 8, 1048576 bytes, linear)
[    0.000000] mem auto-init: stack:off, heap alloc:off, heap free:off
[    0.000000] Memory: 2042704K/2097152K available (4864K kernel code, 1056K rwdata, 1076K rodata, 1216K init, 311K bss, 54448K reserved, 0K cma-reserved)
[    0.000000] SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=2, Nodes=1
[    0.000000] trace event string verifier disabled
[    0.000000] rcu: Hierarchical RCU implementation.
[    0.000000] rcu:     RCU event tracing is enabled.
[    0.000000] rcu:     RCU restricting CPUs from NR_CPUS=256 to nr_cpu_ids=2.
[    0.000000] rcu: RCU calculated value of scheduler-enlistment delay is 25 jiffies.
[    0.000000] rcu: Adjusting geometry for rcu_fanout_leaf=16, nr_cpu_ids=2
[    0.000000] NR_IRQS: 64, nr_irqs: 64, preallocated irqs: 0
[    0.000000] GICv3: 32 SPIs implemented
[    0.000000] GICv3: 0 Extended SPIs implemented
[    0.000000] GICv3: Distributor has no Range Selector support
[    0.000000] Root IRQ handler: gic_handle_irq
[    0.000000] GICv3: 16 PPIs implemented
[    0.000000] GICv3: CPU0: found redistributor 0 region 0:0x0000000020140000
[    0.000000] random: get_random_bytes called from start_kernel+0x504/0x75c with crng_init=0
[    0.000000] arch_timer: cp15 timer(s) running at 25.00MHz (virt).
[    0.000000] clocksource: arch_sys_counter: mask: 0xffffffffffffff max_cycles: 0x5c40939b5, max_idle_ns: 440795202646 ns
[    0.000018] sched_clock: 56 bits at 25MHz, resolution 40ns, wraps every 4398046511100ns
[    0.013330] Console: colour dummy device 80x25
[    0.019751] Calibrating delay loop (skipped), value calculated using timer frequency.. 50.00 BogoMIPS (lpj=100000)
[    0.032834] pid_max: default: 32768 minimum: 301
[    0.041818] Mount-cache hash table entries: 4096 (order: 3, 32768 bytes, linear)
[    0.051435] Mountpoint-cache hash table entries: 4096 (order: 3, 32768 bytes, linear)
[    0.096816] rcu: Hierarchical SRCU implementation.
[    0.109976] EFI services will not be available.
[    0.120556] smp: Bringing up secondary CPUs ...
[    0.138358] CPU features: detected: Spectre-v4
[    0.138565] CPU features: detected: ARM erratum 1418040
[    0.138689] Detected PIPT I-cache on CPU1
[    0.139225] GICv3: CPU1: found redistributor 200 region 0:0x0000000020180000
[    0.139773] CPU1: Booted secondary processor 0x0000000200 [0x413fd0b1]
[    0.141709] smp: Brought up 1 node, 2 CPUs
[    0.181489] SMP: Total of 2 processors activated.
[    0.187553] CPU features: detected: 32-bit EL0 Support
[    0.194117] CPU features: detected: Data cache clean to the PoU not required for I/D coherence
[    0.204902] CPU features: detected: Common not Private translations
[    0.212805] CPU features: detected: CRC32 instructions
[    0.219369] CPU features: detected: RCpc load-acquire (LDAPR)
[    0.226649] CPU features: detected: Privileged Access Never
[    0.233698] CPU features: detected: RAS Extension Support
[    0.240592] CPU features: detected: Speculative Store Bypassing Safe (SSBS)
[    0.251031] CPU: All CPU(s) started at EL1
[    0.256823] alternatives: patching kernel code
[    0.293670] devtmpfs: initialized
[    0.322761] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 7645041785100000 ns
[    0.335579] futex hash table entries: 512 (order: 3, 32768 bytes, linear)
[    0.348861] DMI not present or invalid.
[    0.363142] DMA: preallocated 256 KiB GFP_KERNEL pool for atomic allocations
[    0.373752] DMA: preallocated 256 KiB GFP_KERNEL|GFP_DMA pool for atomic allocations
[    0.384885] DMA: preallocated 256 KiB GFP_KERNEL|GFP_DMA32 pool for atomic allocations
[    0.402211] hw-breakpoint: found 6 breakpoint and 4 watchpoint registers.
[    0.412178] ASID allocator initialised with 65536 entries
[    0.538057] HugeTLB registered 1.00 GiB page size, pre-allocated 0 pages
[    0.546823] HugeTLB registered 32.0 MiB page size, pre-allocated 0 pages
[    0.555371] HugeTLB registered 2.00 MiB page size, pre-allocated 0 pages
[    0.563890] HugeTLB registered 64.0 KiB page size, pre-allocated 0 pages
[    0.583864] wait_for_initramfs() called before rootfs_initcalls
[    0.647083] clocksource: Switched to clocksource arch_sys_counter
[    1.256654] Trying to unpack rootfs image as initramfs...
[    1.452489] workingset: timestamp_bits=46 max_order=19 bucket_order=0
[    1.534497] Freeing initrd memory: 3536K
[    1.632862] squashfs: version 4.0 (2009/01/31) Phillip Lougher
[    1.646062] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 254)
[    1.659869] io scheduler mq-deadline registered
[    1.665965] io scheduler kyber registered
[    2.727778] Serial: 8250/16550 driver, 4 ports, IRQ sharing disabled
[    2.768102] printk: console [ttyS0] disabled
[    2.774263] 20020000.serial: ttyS0 at MMIO 0x20020000 (irq = 13, base_baud = 1562500) is a 16550A
[    2.786150] printk: console [ttyS0] enabled
[    2.786150] printk: console [ttyS0] enabled
[    2.795798] printk: bootconsole [uart8250] disabled
[    2.795798] printk: bootconsole [uart8250] disabled
[    2.815830] cacheinfo: Unable to detect cache hierarchy for CPU 0
[    3.031097] brd: module loaded
[    3.110152] loop: module loaded
[    3.113729] SMCCC: SOC_ID: ARCH_SOC_ID not implemented, skipping ....
[    3.129656] dw-apb-uart 20020000.serial: forbid DMA for kernel console
[    3.146998] Freeing unused kernel memory: 1216K
[    3.168229] Run /init as init process
[    3.172193]   with arguments:
[    3.175391]     /init
[    3.177780]   with environment:
[    3.181125]     HOME=/
[    3.183692]     TERM=linux


BusyBox v1.35.0.git (2021-09-30 14:21:34 CST) built-in shell (ash)
Enter 'help' for a list of built-in commands.

/ # free -h
              total        used        free      shared  buff/cache   available
Mem:           2.0G       20.5M        1.9G        3.5M       10.0M        1.9G
Swap:             0           0           0
/ # cat /proc/cmdline
console=ttyS0,115200 earlycon=uart8250,mmio32,0x20020000 loglevel=10

/proc # cd /proc/device-tree
/sys/firmware/devicetree/base # ls
#address-cells    compatible        model             timer
#size-cells       cpus              name
aliases           interrupt-parent  psci
chosen            memory@102000000  soc
/sys/firmware/devicetree/base # cd chosen
/sys/firmware/devicetree/base/chosen # ls -la
total 0
drwxr-xr-x    2 0        0                0 Jan  1 00:00 .
drwxr-xr-x    9 0        0                0 Jan  1 00:00 ..
-r--r--r--    1 0        0               69 Jan  1 00:01 bootargs
-r--r--r--    1 0        0                8 Jan  1 00:01 linux,initrd-end
-r--r--r--    1 0        0                8 Jan  1 00:01 linux,initrd-start
-r--r--r--    1 0        0                7 Jan  1 00:01 name
-r--r--r--    1 0        0               17 Jan  1 00:01 stdout-path
/sys/firmware/devicetree/base/chosen # cat bootargs
console=ttyS0,115200 earlycon=uart8250,mmio32,0x20020000 loglevel=10
/sys/firmware/devicetree/base/chosen # hexdump -C linux,initrd-start
00000000  00 00 00 01 21 b6 90 00                           |....!...|
00000008
/sys/firmware/devicetree/base/chosen # hexdump -C linux,initrd-end
00000000  00 00 00 01 21 ed d8 00                           |....!...|
00000008
/sys/firmware/devicetree/base/chosen # cat name
chosen
/sys/firmware/devicetree/base/chosen # cat stdout-path
serial0:115200n8
/sys/firmware/devicetree/base/chosen #
```

用 edk2 的 binary 代替 `u-boot.bin` (BL33): 用哪一个 binary?

下面的是以 `edk2-platforms/Platform/ARM/VExpressPkg/ArmVExpress-FVP-AArch64.dsc` 为例:

> The FIP will now contain the additional BL32 image. Here is an example output from an FVP build in release mode including BL32 and using `FVP_AARCH64_EFI.fd` as BL33 image:

    ```
    Firmware Image Package ToC:
    ---------------------------
    - Trusted Boot Firmware BL2: offset=0xD8, size=0x6000
      file: './build/fvp/release/bl2.bin'
    - EL3 Runtime Firmware BL31: offset=0x60D8, size=0x9000
      file: './build/fvp/release/bl31.bin'
    - Secure Payload BL32 (Trusted OS): offset=0xF0D8, size=0x3000
      file: './build/fvp/release/bl32.bin'
    - Non-Trusted Firmware BL33: offset=0x120D8, size=0x280000
      file: '../FVP_AARCH64_EFI.fd'
    ---------------------------
    Creating "build/fvp/release/fip.bin"
    ```

> --- https://github.com/scorp2kk/atf/blob/master/docs/user-guide.md

在FPGA上实验, 由于u-boot只有500多K, `FVP_AARCH64_EFI.fd`有2.5M, 故先要把ATF中 fip size 和 BL33 size的定义更新:

```
/plat/MyCorp/MyChip_fpga/include/platform_def.h
-#define PLAT_NS_IMAGE_MAX_SIZE         ULL(0x100000)
+#define PLAT_NS_IMAGE_MAX_SIZE         ULL(0x280000)
-#define PLAT_MyCorp_FIP_MAX_SIZE       ULL(0x100000)
+#define PLAT_MyCorp_FIP_MAX_SIZE       ULL(0x300000)
```

运行后出现 exception:

```
NOTICE:  Booting Trusted Firmware
NOTICE:  BL1: v2.4(debug):f85ea578c-dirty
NOTICE:  BL1: Built : 09:43:57, Nov  2 2021
INFO:    BL1: RAM 0x207f0000 - 0x207fe000
INFO:    BL1: cortex_a55: CPU workaround for 1530923 was applied
INFO:    BL1: Loading BL2
INFO:    Fip load from memmap dev
INFO:    Loading image id=1 at address 0x207e0000
INFO:    Image id=1 loaded: 0x207e0000 - 0x207e5429
NOTICE:  BL1: Booting BL2
INFO:    Entry point address = 0x207e0000
INFO:    SPSR = 0x3c5
NOTICE:  BL2: v2.4(debug):f85ea578c-dirty
NOTICE:  BL2: Built : 09:43:59, Nov  2 2021
INFO:    BL2: Doing platform setup
INFO:    BL2: Loading image id 3
INFO:    Fip load from memmap dev
INFO:    Loading image id=3 at address 0x100000000
INFO:    Image id=3 loaded: 0x100000000 - 0x100009124
INFO:    BL2: Loading image id 5
INFO:    Fip load from memmap dev
INFO:    Loading image id=5 at address 0x102000000
INFO:    Image id=5 loaded: 0x102000000 - 0x102280000       <== BL33, 2.5M
NOTICE:  BL1: Booting BL31
INFO:    Entry point address = 0x100000000
INFO:    SPSR = 0x3cd
NOTICE:  BL31: v2.4(debug):f85ea578c-dirty
NOTICE:  BL31: Built : 09:44:03, Nov  2 2021
INFO:    GICv3 without legacy support detected.
INFO:    ARM GICv3 driver initialized in EL3
INFO:    Maximum SPI INTID supported: 63
INFO:    BL31: Initializing runtime services
INFO:    BL31: cortex_a55: CPU workaround for 1530923 was applied
INFO:    BL31: Preparing for EL3 exit to normal world
INFO:    Entry point address = 0x102000000                 <== BL33 entry point
INFO:    SPSR = 0x3c5
```

出现exception是预期的(因为FVP和MyChip的配置完全不同). 在`0x102000000`设置断点，第一条为一个跳转指令(`0x14001e1a`反汇编为`b 0x102007868`):
指令`0x14001e1a`的`op`为`b`(无条件跳转), `imm26`为`+0x1e1a`, 即正向跳转, 相对地址距离为 "imm26 times 4"(`0x1e1a<<2=0x7868`), 故跳转后绝对地址为 `0x102000000+0x7968=0x102007868`.

这表明`.Fd`的header最前面包括跳转指令, 而header magic `_FVH` 并不在header的最前面. 这至少说明以`.Fd`为BL33看起来是可信的。

```
00000000: 1a1e 0014 0000 0000 0000 0000 0000 0000  ................
00000010: 78e5 8c8c 3d8a 1c4f 9935 8961 85c3 2dd3  x...=..O.5.a..-.
00000020: 0000 2800 0000 0000 5f46 5648 fffe 0c00  ..(....._FVH....
00000030: 4800 05b2 0000 0002 8002 0000 0010 0000  H...............
00000040: 0000 0000 0000 0000 8317 403e 94cc cd4f  ..........@>...O
00000050: 97bc bd35 ac36 9d2f bfaa 0304 189b 00f8  ...5.6./........
```

另外, pi spec 中关于 flash volume header最前面的`ZeroVector`域的解释也从侧面证实了上面的猜测:

> The first 16 bytes are reserved to allow for the reset vector of processors whose reset vector is at address 0.

```
typedef struct {
    UINT8 ZeroVector[16];
    EFI_GUID FileSystemGuid;
    UINT64 FvLength;
    UINT32 Signature;
    EFI_FVB_ATTRIBUTES_2 Attributes;
    UINT16 HeaderLength;
    UINT16 Checksum;
    UINT16 ExtHeaderOffset;
    UINT8 Reserved[1];
    UINT8 Revision;
    EFI_FV_BLOCK_MAP BlockMap[];
} EFI_FIRMWARE_VOLUME_HEADER;
```

## edk2: create `MyChip` platform

下面的问题就是如何给MyChip建立一个edk2下的platform.

refs:

- [stackoverflow question](https://stackoverflow.com/questions/69807637/is-there-a-guide-on-porting-edk2-to-a-new-arm64-platform)
- [old edk2 repo with documentation](https://bitbucket.org/incubaid/edk2/src/master/ArmPlatformPkg/Documentation/): also exists in `UDK2014` branch of `edk2` repo
- [Porting UEFI to BeagleBoneBlack, brief notes](https://varadgautam.wordpress.com/2014/07/14/porting-uefi-to-beagleboneblack-1/)

What's the difference between `edk2` and `edk2-platforms` repos? Particularly, both contains ARM related directories, what's the relationship?

> The intent is for packages in edk2-platforms to be CPU, Chipset, SoC, or platform specific. Drivers that are CPU arch and platform agnostic should be put into the edk2 repo.
>
> --- https://github.com/tianocore/edk2-platforms/blob/about/Readme.md

According the following quote, for MyChip (as a platform), it seems that we should create a directory `edk2-platform/Platform/MyCorp/MyChip/`, and put related dsc/fdf/dec files, together with platform specific implementations (if any) there.

FIXME: `edk2-platforms/Silicon/` may contain cpu/chip related stuff, (e.g., `Phytium`).

> Platform description files can be found under Platform/{Vendor}/{Platform}.
>
> --- https://github.com/tianocore/edk2-platforms/blob/master/Readme.md

```
$ mkdir -p edk2-platforms/Platform/MyCorp/MyChip
```

以 `./edk2-platform/Platform/RaspberryPi/RPi4/` 为模板:

- RPi4 is a `ATF+UEFI` approach, i.e., UEFI firmware acts as BL33. Another example is [BlueField](https://docs.mellanox.com/display/BlueFieldSWv31011424/Installation+and+Initialization):

    ```{r echo=FALSE, out.width='80%', fig.align='center', fig.pos = 'h', fig.cap="ATF+UEFI firmware integration approach"}
    knitr::include_graphics("./images/atf-uefi-boot-process.png")
    ```

    - Some info can be found from old document in branch `UDK2014` under `ArmPlatformPkg/Documentation/ArmPlatformPkg.txt`. It seems that there are two ways for porting UEFI to ARM platform:
        - full boot: the UEFI firmware starts from XIP memory and in secure world. Boot sequence: Sec/PrePiCore/PeiCore/Dxe/Bds.
        - 2nd stage boot: memory has already been initialized by the 1st stage boot loader. Boot sequence: ATF(BL1/2/31)/PrePi/Dxe/Bds.
        - Apparently, RPi4's `ATF+UEFI` approach is the 2nd choice.
    - Interface between ATF and UEFI firmware:
        - One of the hard-coded i/f: the BL33 entry point address (let's call it `bl33_base_addr`).
            - `bl33_base_addr` is defined in ATF: so BL2 loads BL33 from fip to this physical address.
            - in edk2, `bl33_base_addr` maps to `BaseAddress` in `MyChip.fdf`:

                ```
                [FD.Test]
                  BaseAddress   = 0x102000000|gArmTokenSpaceGuid.PcdFdBaseAddress
                  Size          = 0x0001f0000|gArmTokenSpaceGuid.PcdFdSize
                ```
            - Notice that, according to [FDF spec](https://edk2-docs.gitbook.io/edk-ii-fdf-specification/2_fdf_design_discussion/21_processing_overview#pcd-rules), the `BaseAddress`/`Size` are also automatically assigned to PCD values. The PCD values are referenced in `edk2/ArmPlatformPkg/PrePi/AArch64/ModuleEntryPoint.S:30` via `FixedPcdGet()` function. If the values are not assigned to respective PCD values, the default PCD values (`0`) will be taken when compiling `ModuleEntryPoint.S` (which will fail).
        - Other i/f info (convey via PCD): inspect the PCD section of build report. Check each value to see if it make sense to the platform.
- Prepare an empty pkg, and make it build ok.
    - Make a copy of `RaspberryPi.dec`, change all `gRaspberry` to `gMyChip`.
    - Make a copy of `RPi4.dsc` and `RPi4.fdf`, and comment out all stuff in `DSC` and `FDF` file.
    - Replace all GUIDs in `DSC`/`FDF`/`DEC` files, generating new one using [online guid generator](https://guidgenerator.com/).
    - Note that PCD are declared in `DEC` files, and DEC files are refered by modules (`INF` files). As the empty package contains no module, no PCD definition will be available in `FDF`. So for a success build of the empty package, we need to comment out all PCD reference in `FDF`.
    - The `NOOPT` build command for MyChip is as below:

        ```
        #!/bin/bash

        export WORKSPACE=/home/bruin/work/tianocore
        export PACKAGES_PATH=$WORKSPACE/edk2:$WORKSPACE/edk2-platforms:$WORKSPACE/edk2-non-osi
        pushd $WORKSPACE
        source edk2/edksetup.sh

        echo "Building BaseTools..."
        make -C edk2/BaseTools all

        echo "Building UEFI firmware for MyChip..."
        GCC5_AARCH64_PREFIX=aarch64-none-linux-gnu- build \
              -n 4 \
              -a AARCH64 \
              -p Platform/MyCorp/MyChip/MyChip.dsc \
              -t GCC5 \
              -b NOOPT \
              -v -d 9 -j MyChip-build.log \
              -y MyChip-build-report.txt \
              -Y EXECUTION_ORDER \
              -Y PCD \
              -Y LIBRARY \
              -Y DEPEX \
              -Y HASH \
              -Y BUILD_FLAGS \
              -Y FLASH \
              -Y FIXED_ADDRESS \
              all
        popd
        ```

### Increase BL33/FIP size

```
plat/MyCorp/MyChip_fpga/include/platform_def.h:
-#define PLAT_NS_IMAGE_MAX_SIZE         ULL(0x100000)
+#define PLAT_NS_IMAGE_MAX_SIZE         ULL(0x200000)
-#define PLAT_MyCorp_FIP_MAX_SIZE       ULL(0x100000)
+#define PLAT_MyCorp_FIP_MAX_SIZE       ULL(0x280000)
```

### Add the 1st module `ArmPlatformPrePiUniCore`

Add the first `[Components]`: `ArmPlatformPkg/PrePi/PeiUniCore.inf`, which is of `MODULE_TYPE = SEC`.

- What's this component: this is the first (and only) `SEC` (Security) module in RPi4. What the name `PrePi` and `Pei` implies?

    > ... the PI spec is not tied to edk2 PEIMs, and I don't see where EDKII PEI modules are currently the only "acknowledged" silicon init environment. The edk2 tree itself seems to contain platforms that don't use the edk2 PEI module set at all, but (IIRC) jump from SEC to DXE. I believe "ArmPlatformPkg/PrePi" and "ArmVirtPkg/PrePi" are related to this.
    >
    > --- https://listman.redhat.com/archives/edk2-devel-archive/2020-November/msg00021.html

- Its entry point: all UEFI components have the same entry point (`_ModuleEntryPoint`).
    - By "component", it means either a UEFI driver and UEFI app, both are PE32 executables, usually with suffix `.efi`.
    - The `.efi`s are converted from ELF executables (`.dll`) by `GenFw` tool: modifying the file headers.
    - To verify that "all components' entry point is `_ModuleEntryPoint`":
        - Check the `.dll` generating command line in build report (`build -y <BUILD_REPORT_FILE>`), we have two flags `"aarch64-none-linux-gnu-gcc" -o xxx.dll -u _ModuleEntryPoint -Wl,-e,_ModuleEntryPoint ...`:
            - `-u`: `gcc --help -v|grep "undefined SYMBOL"` gives `-u SYMBOL --undefined SYMBOL: star with undefined reference to SYMBOL`.
            - `Wl,-e`: `ld --help|grep "entry"` gives `-e ADDRESS, --entry ADDRESS Set start address`.
        - Check all `.dll` files that `Entry point address == _ModuleEntryPoint`: `find . -type f -name "*.dll" -exec sh -c "readelf -a {} |grep -E 'Entry point address|_ModuleEntryPoint'" \;`
- Its entry point is the entry point of whole UEFI FD image (i.e., from `bl33_base_addr` jump to this `_ModuleEntryPoint`):

    > Topology of the UEFI Firmware File
    >
    > A UEFI Firmware File (actually a UEFI Firmware Device - FD file) is a collection of UEFI binaries encapsulated into a single image. The format of this image is defined by the Platform Initialization Specification Volume 3. A Vector Table is located at the base of this file. A 'BL' branch instruction at the base of the firwmare (location of the Reset Entry into the Vector Table) will jump to the first 'SEC' module of the UEFI Firmware Image.
    >
    > --- https://github.com/lzeng14/tianocore/wiki/ArmPkg-Debugging

    - To verify the statements above:

        - Disassember the reset vector (i.e., the 1st word) of generated `.FD` (we got offset=`0x360`):

            ```
            $ xxd -l 4 -e TEST.fd       <== dump 4 bytes in little endian
            00000000: 140000d8          <== BL   {PC}+(0xd8<<2); offset=0x360
            ```

        - Check the Entry point in `.dll` (we got offset=`0x240`):

            ```
            $ aarch64-none-elf-objdump -t ArmPlatformPrePiUniCore.dll|grep _ModuleEntryPoint
            0000000000000240 g     F .text  0000000000000000 _ModuleEntryPoint
            $ readelf -h ArmPlatformPrePiUniCore.dll|grep Entry
              Entry point address:               0x240
            ```

        - Compare contents of two files at different offset (we got identicial content):

            ```
            $ xxd -s 0x360 -l 64 TEST.fd                      <== skip 0x360 bytes, dump 64 bytes
            00000360: 901e 0094 050a 0094 ea03 00aa a1cd 0a58  ...............X
            00000370: 0200 e0d2 2200 c0f2 0240 a0f2 0200 80f2  ...."....@......
            00000380: c303 a0d2 e3ff 9ff2 6304 00d1 6300 028b  ........c...c...
            00000390: 0400 a1d2 0400 80f2 2000 03eb 8400 0054  ........ ......T
            $ xxd -s 0x240 -l 64 ArmPlatformPrePiUniCore.dll  <== skip 0x240 bytes
            00000240: 901e 0094 050a 0094 ea03 00aa a1cd 0a58  ...............X
            00000250: 0200 e0d2 2200 c0f2 0240 a0f2 0200 80f2  ...."....@......
            00000260: c303 a0d2 e3ff 9ff2 6304 00d1 6300 028b  ........c...c...
            00000270: 0400 a1d2 0400 80f2 2000 03eb 8400 0054  ........ ......T
            ```
    - call sequence analysis (from SEC to DXE):

        ```
        _ModuleEntryPoint()                <= edk2/ArmPlatformPkg/PrePi/AArch64/ModuleEntryPoint.S
        `- CEntryPoint()                   <= edk2/ArmPlatformPkg/PrePi/PrePi.c
            `- PrimaryMain()               <= edk2/ArmPlatformPkg/PrePi/MainUniCore.c
                `- PrePiMain()             <= edk2/ArmPlatformPkg/PrePi/PrePi.c
                    `- LoadDxeCoreFromFv() <= edk2/EmbeddedPkg/Library/PrePiLib/PrePiLib.c
        ```

    - Related: [edk2 app 入口分析](http://www.lab-z.com/22applicationentry/)
    - FIXME: under `edk2/ArmPlatformPkg/PrePi/` there are two implementations: "UniCore" and "MPCore". What's the difference and why RPi4 chose UniCore? Probably `BL33` is only supposed to be run on the primary core...

- Its direct-lib-class-dependencies are listed in `INF` file (`ArmPlatformPkg/PrePi/PeiUniCore.inf`): totally 18 lib-classes (line 43 and 50 are duplicates).

    ```
    39 [LibraryClasses]
    40   BaseLib
    41   CacheMaintenanceLib
    42   DebugLib
    43   DebugAgentLib
    44   ArmLib
    45   IoLib
    46   TimerLib
    47   SerialPortLib
    48   ExtractGuidedSectionLib
    49   LzmaDecompressLib
    50   DebugAgentLib
    51   PrePiLib
    52   ArmPlatformLib
    53   ArmPlatformStackLib
    54   MemoryAllocationLib
    55   HobLib
    56   PrePiHobListPointerLib
    57   PlatformPeiLib
    58   MemoryInitPeiLib
    ```

- Its complete lib class dependencies (as well as the actual lib instances) can be found in the pkg build report. Totally 34 libraries. Note that the same info can also be found in build log.

    |P?|class|instance|
    |--|:----|:-------|
    ||NULL|./edk2/MdeModulePkg/Library/LzmaCustomDecompressLib/LzmaCustomDecompressLib.inf|
    ||NULL|./edk2/MdePkg/Library/BaseStackCheckLib/BaseStackCheckLib.inf|
    ||DebugPrintErrorLevelLib|./edk2/MdePkg/Library/BaseDebugPrintErrorLevelLib/BaseDebugPrintErrorLevelLib.inf|
    ||ReportStatusCodeLib|./edk2/MdePkg/Library/BaseReportStatusCodeLibNull/BaseReportStatusCodeLibNull.inf|
    ||PcdLib|./edk2/MdePkg/Library/BasePcdLibNull/BasePcdLibNull.inf|
    ||BaseMemoryLib|./edk2/MdePkg/Library/BaseMemoryLib/BaseMemoryLib.inf|
    ||CompilerIntrinsicsLib|./edk2/ArmPkg/Library/CompilerIntrinsicsLib/CompilerIntrinsicsLib.inf|
    ||LibSoftfloat|./edk2-libc/StdLib/LibC/Softfloat/Softfloat.inf|
    ||DebugLib|./edk2/MdeModulePkg/Library/PeiDxeDebugLibReportStatusCode/PeiDxeDebugLibReportStatusCode.inf|
    ||BaseLib|./edk2/MdePkg/Library/BaseLib/BaseLib.inf|
    ||ArmLib|./edk2/ArmPkg/Library/ArmLib/ArmBaseLib.inf|
    ||RegisterFilterLib|./edk2/MdePkg/Library/RegisterFilterLibNull/RegisterFilterLibNull.inf|
    ||PeCoffExtraActionLib|./edk2/ArmPkg/Library/DebugPeCoffExtraActionLib/DebugPeCoffExtraActionLib.inf|
    ||PrePiHobListPointerLib|./edk2/ArmPlatformPkg/Library/PrePiHobListPointerLib/PrePiHobListPointerLib.inf|
    ||IoLib|./edk2/MdePkg/Library/BaseIoLibIntrinsic/BaseIoLibIntrinsic.inf|
    ||ArmGenericTimerCounterLib|./edk2/ArmPkg/Library/ArmGenericTimerPhyCounterLib/ArmGenericTimerPhyCounterLib.inf|
    ||PerformanceLib|./edk2/MdePkg/Library/BasePerformanceLibNull/BasePerformanceLibNull.inf|
    ||PeCoffLib|./edk2/MdePkg/Library/BasePeCoffLib/BasePeCoffLib.inf|
    ||UefiDecompressLib|./edk2/MdePkg/Library/BaseUefiDecompressLib/BaseUefiDecompressLib.inf|
    ||PrintLib|./edk2/MdePkg/Library/BasePrintLib/BasePrintLib.inf|
    ||HobLib|./edk2/EmbeddedPkg/Library/PrePiHobLib/PrePiHobLib.inf|
    ||ExtractGuidedSectionLib|./edk2/EmbeddedPkg/Library/PrePiExtractGuidedSectionLib/PrePiExtractGuidedSectionLib.inf|
    ||TimerLib|./edk2/ArmPkg/Library/ArmArchTimerLib/ArmArchTimerLib.inf|
    ||CacheMaintenanceLib|./edk2/MdePkg/Library/BaseCacheMaintenanceLib/BaseCacheMaintenanceLib.inf|
    ||PrePiLib|./edk2/EmbeddedPkg/Library/PrePiLib/PrePiLib.inf|
    ||FdtLib|./edk2/EmbeddedPkg/Library/FdtLib/FdtLib.inf|
    ||MemoryAllocationLib|./edk2/EmbeddedPkg/Library/PrePiMemoryAllocationLib/PrePiMemoryAllocationLib.inf|
    ||ArmMmuLib|./edk2/ArmPkg/Library/ArmMmuLib/ArmMmuBaseLib.inf|
    ||DebugAgentLib|./edk2/MdeModulePkg/Library/DebugAgentLibNull/DebugAgentLibNull.inf|
    ||ArmPlatformStackLib|./edk2/ArmPlatformPkg/Library/ArmPlatformStackLib/ArmPlatformStackLib.inf|
    ||PlatformPeiLib|./edk2/ArmPlatformPkg/PlatformPei/PlatformPeiLib.inf|
    |*|SerialPortLib|./edk2-platforms/Silicon/Hisilicon/Library/Dw8250SerialPortLib/Dw8250SerialPortLib.inf|
    |*|MemoryInitPeiLib|./edk2-platforms/Platform/RaspberryPi/Library/MemoryInitPeiLib/MemoryInitPeiLib.inf|
    |*|ArmPlatformLib|./edk2-platforms/Platform/RaspberryPi/Library/PlatformLib/PlatformLib.inf|

    - Btw, the table is generated by a sequence of `sed` commands when extracting info from build-report. However, as a hindersight, it will be much easier to extract the same info from build-log.

        ```
        $ cp build-report.txt libs.txt
        $ vi libs.txt                                        # only keep the libs for the module
        $ sed -e "s/^{\(.*\):.*$/\1/" libs.txt > 1.txt       # trim LibraryClass line
        $ sed -n -e '$!{x;n;G;}' -e 'p' 1.txt > 2.txt        # swap line order from instance/class to class/instance
        $ sed 'N;s/\n/|/' 2.txt > 3.txt                      # concat class and instance lines, and insert | in betw
        $ sed -e 's/^/||/'  3.txt > 4.txt                    # insert an empty column at beginning
        $ sed -e 's/$/|/'  4.txt > 5.txt                     # complete the last column
        $ vi 5.txt                                           # add the table header
        ```

    - All edk2 components (including this one) are statically linked (just `file` or `ldd` against the `.dll` files).

        > Using the classic definition of static linking, like your example, all EFI modules are statically linked.
        >
        > Libraries are linked as objects, that can be linked into Modules. Modules are linked into relocatable PE/COFF images.
        >
        > --- https://edk2-devel.narkive.com/fFgVA7Ws/static-link-dynamic-link-question

    - The `P?` column in the table above indicates whether or not the lib instance is platform-specific, i.e., needs to be customized according to the actual platform MyChip.

    - How to add the module into the pkg? The following is rather a generic procedure for adding any component.
        - Add the module's `INF` into both `DSC` (`[Components]` section), and `FDF` (`[FV.FVMAIN_COMPACT]`).
        - Rebuild the pkg, and resolve all `Instance of library class [xxxLib] is not found` errors reported, by updating `[LibraryClasses]` sections of `DSC`.
            - This step is a repeating process for dozens of times.
            - Some lib-class has multiple lib-instances, making sure choose the appropriate lib-instance (ref the build-report of RPi4).
            - if encounter `ModuleEntryPoint.iiii:31: Error: immediate out of range`: enable `gArmTokenSpaceGuid.PcdFdBaseAddress` and `gArmTokenSpaceGuid.PcdFdSize` in `FDF`.
            - if encounter `undefined reference to _gPcd_BinaryPatch_PcdSerialClockRate`: set `PcdSerialClockRate` in `[PcdsPatchableInModule]` section in `DSC`. FIXME: why? [ref](https://edk2-docs.gitbook.io/edk-ii-dsc-specification/3_edk_ii_dsc_file_format/39_pcd_sections).
        - Check the PCDs listed in build log: inspect any abnormal PCD values, and supply correct values (ref to RPi4).
        - Customize platform-specific drivers.
            - `SerialPortLib`: locate the lib-class header file (`MdePkg/Include/Library/SerialPortLib.h`) by `find edk2 -type f -name "*.dec" -exec grep -Hn SerialPortLib`. The following functions are required:
                - `SerialPortInitialize()`
                - `SerialPortWrite()`
                - `SerialPortRead()`
                - `SerialPortPoll()`
                - `SerialPortSetControl()`: RETURN_UNSUPPORTED
                - `SerialPortGetControl()`: RETURN_UNSUPPORTED
                - `SerialPortSetAttributes()`: RETURN_UNSUPPORTED
            - `ArmPlatformLib`: interface header at `Include/Library/ArmPlatformLib.h`. The following functions are required:
                - `ArmPlatformGetCorePosition()`: return cpu idx in the cluster given the MPIDR value. this function is used in `_ModuleEntryPoint` for setting stack for secondary cores. Assuming one cluster for now.
                - `ArmPlatformIsPrimaryCore()`
                - `ArmPlatformGetPrimaryCoreMpId()`
                - `ArmPlatformGetBootMode()`
                - `ArmPlatformPeiBootAction()`
                - `ArmPlatformInitialize()`
                - `ArmPlatformGetVirtualMemoryMap()`
                - `ArmPlatformGetPlatformPpiList()`
            - `MemoryInitPeiLib`: seems the interface header is missing?
- How PCD works?
    - [FAQ](https://github.com/lersek/edk2/wiki/PCD)
    - [PCD access methods](https://edk2-docs.gitbook.io/edk-ii-build-specification/8_pre-build_autogen_stage/82_auto-generation_process#8.2.4.8-pcd-access-methods)

    > Books like Beyond BIOS by Vincent Zimmer, Michael Rothman, and Suresh Marisetty (Intel Press, 2011) describe the specifications, but there hasn’t been a single place to describe the implementation. The next section is intended to help with that gap.
    >
    > --- [Building Firmware for Quark Processors](https://link.springer.com/content/pdf/10.1007%2F978-1-4842-0070-4_7.pdf)

    - for each PCD variable, uniquely identified by `<token_space_id>.<token_id>`, has the following attributes:
        - token space id: GUIDed name space
        - token id: numerical id for the variable
        - CNames: token_space_id and token_id has corresponding CNames.
        - pcd type (aka "access method"): five types are defined in edk2.
            - static config: determined at build time (or modified prior to insert a module into Flash, as for `PatchableInModule`).
              - FeatureFlag: used for enable some code paths. no storage in final images.
              - FixedAtBuild: : Replaces a macro that produced a customizable value. The value of this PCD type is determined at build time and is stored in the code section of a module’s PE image.
              - PatchableInModule: The value is stored in the data section, rather than the code section, of the module’s PE image.
            - dynamic config: a config knob can be manipulated at runtime (by e.g., setup screen). The value is assigned by one module and is accessed by other modules in execution time.
              - Dynamic:
              - DynamicEx: this is the only access method defined by PI spec.
              - DynamicHii:
              - DynamicVpd:
            - A PCD may be listed under multiple access method sections (except `FeatureFlag` type) in `DEC` file. Doing so indicates that modules have been coded to use the PCD in any of the non-`FeatureFlag` access method.
        - data type: the data type of the PCD, such as bool, int, string, struct, etc
        - value: the value of the corresponding data type. for a module at build time, the value is taken in the following precedence:
            - default value (optional) in `INF`
            - command line of `build` utility
            - from `FDF`
            - from `DSC`
            - from `DEC`
        - storage:
        - module-association:
            - source code modules:
            - binary only modules: PatchableInModule and DynamicEx
        - value producers:
        - value consumers:
        - pcd variables are:
            - declared:
                - in DEC: `TokenSpaceGuidCName.TokenCName|DefaultValue|DataType|TokenId`, as well as its access methods (indicated by the section name). The DEC file is part of a pkg. Any pkg may define PCD entries. Any module that depends on a pkg may use the PCD entries defined in that pkg's DEC file.
                - in `AugoGen.h`
            - defined in `AutoGen.c`
            - accessed:
                - in INF: defines what PCD are being used within the module as well as the access method, and optionally overriding default value.
                - in DSC: override default value, as well as specifing access method. Cannot conflict with established restrictions.
                - in FDF: override default value
                - in `*.c`: use appropriate get/set function(macro) corresponding to the access method(s).
- call sequence anaysis (`aarch64-none-elf-objdump -S ArmPlatformPrePiUniCore.debug > ArmPlatformPrePiUniCore.dump`):

    ```
    _ModuleEntryPoint     <= ArmPlatformPkg/PrePi/AArch64/ModuleEntryPoint.S
    |-- ArmPlatformPeiBootAction
    |-- ArmReadMpidr
    |-- _SetSVCMode:
    |-- _SetupStackPosition:
    |-- _SetupStack:
    |-- _SetupAlignedStack:
    |-- _SetupOverflowStack:
    |-- _GetBaseUefiMemory:
    |-- _GetStackBase:
    |   |-- ArmPlatformStackSet
    |   `-- ArmPlatformIsPrimaryCore
    |-- _PrepareArguments
    |   |-- x0 = MpID
    |   |-- x1 = UefiMemoryBase
    |   `-- x2 = StacksBase
    `-- CEntryPoint            <= ArmPlatformPkg/PrePi/PrePi.c
        |-- ArmPlatformInitialize()
        |-- ArmDisableDataCache()
        |-- ArmInvalidateInstructionCache()
        |-- ArmEnableInstructionCache()
        |-- InvalidateDataCacheRange()
        `-- PrimaryMain()      <= ArmPlatformPkg/PrePi/MainUniCore.c
            `-- PrePiMain()    <= ArmPlatformPkg/PrePi/PrePi.c
                |-- ArchInitialize()
                |   `-- ArmEnableVFP()
                |-- SerialPortInitialize()                    <= MyChip/Library/DwApbSerialPortLib/DwApbSerialPortLib.c
                |-- SerialPortWrite("UEFI firmware (version %s built at %a on %a)")
                |-- InitializeDebugAgent()
                |-- SaveAndSetDebugTimerInterrupt()
                |-- HobConstructor()      # construct the 1st Hob (EFI_HOB_TYPE_HANDOFF)
                |-- PrePeiSetHobList()    # use TPIDR_EL0 to store HobList addr
                |-- MemoryPeim()                              <= MyChip/Library/MemoryInitPeiLib/MemoryInitPeiLib.c
                |   |-- ArmPlatformGetVirtualMemoryMap()      <= MyChip/Library/PlatformLib/MyChipMem.c
                |   |-- MyChipPlatformGetVirtualMemoryInfo()
                |   |-- InitMmu()
                |   |   `-- ArmConfigureMmu()                 <= ArmMmuLibCore.c: 1:1 mapping, 4K page
                |   `-- BuildMemoryTypeInformationHob()
                |       `-- BuildGuidDataHob()
                |           `-- BuidGuidHob()  # Hob type: EFI_HOB_TYPE_GUID_EXTENSION
                |-- BuildStackHob()            # Hob type: EFI_HOB_TYPE_MEMORY_ALLOCATION
                |-- BuildCpuHob()              # Hob type: EFI_HOB_TYPE_CPU
                |-- if (ArmIsMpCore())
                |   |-- ...
                |   |-- BuildGuidDataHob(&gArmMpCoreInfoGuid...)
                |   `-- ...
                |-- GetTimeInNanoSecond()
                |-- BuildGuidDataHob(&gEfiFirmwarePerformanceGuid...)
                |-- SetBootMode(BOOT_WITH_FULL_CONFIGURATION)  # Update PHIT (i.e., the 1st Hob)
                |-- PlatformPeim()    <= ArmPlatformPkg/PlatformPei/PlatformPeiLib.c
                |   `-- BuildFvHob()  # Hob type: EFI_HOB_TYPE_FV
                |-- ProcessLibraryConstructorList()
                |-- DecompressFirstFv()
                `-- LoadDxeCoreFromFv()   # search EFI_FV_FILETYPE_DXE_CORE (5)
                    `-- LoadDxeCoreFromFfsFile()
                        |-- FfsFindSectionData (EFI_SECTION_PE32,...)
                        |-- LoadPeCoffImage(...,&EntryPoint)
                        |-- FfsGetFileInfo()
                        |-- BuildModuleHob()
                        |-- "Loading DxeCore at 0x%10p EntryPoint=0x%10p\n"
                        |-- ...
                        `-- SwitchStack(EntryPoint, Hob, NULL, TopOfStack)
                            `-- DxeMain(Hob)
    ```
- Porting results: 2021.11.22 (commit `f5e4e04a` on personal repo): before customizing `ArmPlatformGetVirtualMemoryMap()`, first try UART on FPGA. And UART seems working.

    ```
    ...
    INFO:    Loading image id=5 at address 0x102000000
    INFO:    Image id=5 loaded: 0x102000000 - 0x1020e0000
    NOTICE:  BL1: Booting BL31
    INFO:    Entry point address = 0x100000000
    INFO:    SPSR = 0x3cd
    NOTICE:  BL31: v2.4(debug):f85ea578c
    NOTICE:  BL31: Built : 14:40:37, Nov 22 2021
    INFO:    GICv3 without legacy support detected.
    INFO:    ARM GICv3 driver initialized in EL3
    INFO:    Maximum SPI INTID supported: 63
    INFO:    BL31: Initializing runtime services
    INFO:    BL31: cortex_a55: CPU workaround for 1530923 was applied
    INFO:    BL31: Preparing for EL3 exit to normal world
    INFO:    Entry point address = 0x102000000
    INFO:    SPSR = 0x3c5
    UEFI firmware (version EDK2-DEV built at 14:33:16 on Nov 22 2021)
    ArmPlatformGetVirtualMemoryMap() must be called before MyChipPlatformGetVirtualMemoryInfo().
    ```

    After updating memory map (via PCD), at `a73b40c2`, it seems that the values for the memory map regions are good (adding some debug in `PrePiMain()`):

    ```
    UEFI firmware (version EDK2-DEV built at 17:27:48 on Nov 22 2021)
    UefiMemoryBase=0x1BE0F0000
    StacksBase=0x1C20E9000
    mSystemMemoryBase=0x1020F0000
    mSystemMemoryEnd=0x1C20EFFFF
    ROM:
            PhysicalBase: 0x0
            VirtualBase: 0x0
            Length: 0x10000
    SRAM:
            PhysicalBase: 0x20400000
            VirtualBase: 0x20400000
            Length: 0x400000
    FD:
            PhysicalBase: 0x102000000
            VirtualBase: 0x102000000
            Length: 0xC0000
    FD Variables:
            PhysicalBase: 0x1020C0000
            VirtualBase: 0x1020C0000
            Length: 0x20000
    Flattened Device Tree:
            PhysicalBase: 0x1020E0000
            VirtualBase: 0x1020E0000
            Length: 0x10000
    System RAM in DDR0:
            PhysicalBase: 0x1020F0000
            VirtualBase: 0x1020F0000
            Length: 0xC0000000
    MMIO Device:
            PhysicalBase: 0x20000000
            VirtualBase: 0x20000000
            Length: 0x200000
    MemoryPeim() ok!
    BuildStackHob() ok!
    BuildCpuHob() ok!
    ArmIsMpCore() enters.
    before GetTimeInNanoSeconds()
    after GetTimeInNanoSeconds()
    after BuildGuidDataHob()
    after SetBootMode()
    after PlatformPeim()
    after ProcessLibraryConstructorList()

    ASSERT_EFI_ERROR (Status = Not Found)
    ASSERT [ArmPlatformPrePiUniCore] /home/bruin/work/tianocore/edk2/ArmPlatformPkg/PrePi/PrePi.c(168): !(((INTN)(RETURN_STATUS)(Status)) < 0)
    ```

    The error occured in `DecompressFirstFv()`, which is expected since there is no compressed FV in the FD at the moment.

- Memory layout: RPi4 UEFI image size is `0x1b0000`, we take `0x1e0000` as max size for MyChip. So `MyChip.fd` (BL33) size is `0x200000` (plus 128K variables). FIP contains BL2+BL31+MyChip.fd, we reserve 512K for BL2+BL31, so:

    - `PLAT_NS_IMAGE_MAX_SIZE   = 0x200000`;
    - `PLAT_MyCorp_FIP_MAX_SIZE = 0x280000`;

    ```
    |<----- fip.bin: 2.5MiB ----------------->|
                 |<----- MyChip.fd: 2MiB ---->|

    +-----+------+----------------------------+
    | BL2 | BL31 |    BL33(MyChip.fd)         |
    +-----+------+----------------------------+
    ```

    Inside the `MyChip.fd`:

    ```
    |<--- MyChip.fd: 0x200000 ---------------------------------->|
    |<--- FVMAIN_COMPACT: 0x1E0000 --->|<-- Variable: 0x20000 -->|

    +----------------------------------+-----+-----+-----+-------+
    |  FVMAIN_COMPACT                  | Var | Evt | Ftw | Ftw   |
    +----------------------------------+-----+-----+-----+-------+
                                         56K   4K    4K     64K
    ```

    Btw, in RAM, FDT is placed right after BL33, size is 64K.

    According to `ArmPlatformPkg/PrePi/AArch64/ModuleEntryPoint.S`, the memory layout is as below:

    ```
                  +-------------------------------+ DDR top
                  |                               |
                  z                               z
                  |                               |
    0x1_C20F_0000 +-------------------------------+ mSystemMemoryEnd
                  | PcdSystemMemoryUefiRegionSize | StacksBase
                  |     (0x04000000=64M)          |
    0x1_BE0F_0000 +-------------------------------+ UefiMemoryBase
                  |                               |
                  z                               z
                  |                               |
    0x1_0221_0000 +-------------------------------+ PcdSystemMemoryBase
                  |          dtb (64K)            |
    0x1_0220_0000 +-------------------------------+ FdTop
                  |      variables (128K)         |
    0x1_021E_0000 |-----                     -----|
                  |                               |
                  |       PcdFdSize (2M)          |
    0x1_0200_0000 +-------------------------------+ PcdFdBaseAddress
                  |                               |
    0x1_0000_0000 +-------------------------------+ DDR base
    ```

    The top 64M (`PcdSystemMemoryUefiRegionSize`) up to `mSystemMemoryEnd` is reserved for UEFI, and the top `0x7000` byte (28K) within this 64M is for stacks (16K for the primary cpu, and 4K for each secondary cpu). MMU setting for UEFI is identity (1:1) mapping.
- [ArmPkg debugging](https://github.com/lzeng14/tianocore/wiki/ArmPkg-Debugging)
    - change DEBUG print level by setting `PcdDebugPrintErrorLevel` according to `DEBUG_XXX` flags defined in `MdePkg/Include/Library/DebugLib.h`.

### Add the 2nd module: `DxeCore`

- FD organization:

    ```
    MyChip.fd: 2M
    |-- FVMAIN_COMPACT: 1.8M
    |   |-- ArmPlatformPrePiUniCore
    |   `-- FVMAIN: nested and compressed FV
    |       |-- DxeCore
    |       |-- PcdCore
    |       |-- ArmCpuDxe
    |       |-- RuntimeDxe
    |       |-- ...
    |-- NV_VARIABLE_STORE: 56k
    |-- NV_EVENT_LOG: 4k
    |-- NV_FTW_HEADER: 4k
    `-- NV_FTW_DATA: 64k
    ```
- Add `DxeCore`: `DecompressFirstFv()` failed.

    ```
    `DecompressFirstFv()`
    |-- FfsAnyFvFindFirstFile()
    |   |-- GetHobList()
    |   |-- GetNextHob()
    |   |-- CompareGuid()
    |   |-- FfsFindSectionData()
    |   |-- FfsGetVolumeInfo()
    |   |-- BuildFvHob()
    |   `-- BuildFv2Hob()
    `-- FfsProcessFvFile()
        |-- FfsFindSectionData()
        |   `-- FfsProcessSection()   # UefiDecompress() happens here
        |-- FfsGetVolumeInfo()
        |-- AllocateAlignedPages()
        |-- CopyMem()
        |-- FfsGetVolumeInfo()
        |-- BuildFvHob()
        `-- BuildFv2Hob()
    ```

    Debug output (2021.11.24):

    ```
    after ProcessLibraryConstructorList()
    FfsFindNextVolume() enters: Instance=0
         ok. Instance=-1
    FfsFindNextVolume() ok. Instance=1, VolumeHandle=0x1C20EFEA0
    FfsFindNextFile(file_type=11) failed. Instance=1
    FfsFindNextVolume() enters: Instance=1

    ASSERT_EFI_ERROR (Status = Not Found)
    ASSERT [ArmPlatformPrePiUniCore] /home/bruin/work/tianocore/edk2/EmbeddedPkg/Library/PrePiLib/FwVol.c(564): !(((INTN)(RETURN_STATUS)(((RETURN_STATUS)(0x8000000000000000ULL | (14))))) < 0)
    ```

- The bug is caused by not setting `PcdFvBaseAddress` and `PcdFvSize` correctly. After fix that (commit `38775def`), we got the following debug output (2021.11.25):

    ```
    ArmIsMpCore() enters.
    before GetTimeInNanoSeconds()
    after GetTimeInNanoSeconds()
    after BuildGuidDataHob()
    after SetBootMode()
    PcdFvBaseAddress=0x102000000, PcdFvSize=0xC0000
    after PlatformPeim()
    after ProcessLibraryConstructorList()
    FfsFindNextVolume() enters: Instance=0
            ok. Instance=-1. BaseAddress=0x102000000, Length=0xC0000
    FfsFindNextVolume() return ok. Instance=1, VolumeHandle=0x102000000
    FfsFindNextFile(file_type=11) ok. Instance=1. Return to caller.
    after DecompressFirstFv()
    FfsFindNextVolume() enters: Instance=0
            ok. Instance=-1. BaseAddress=0x102000000, Length=0xC0000
    FfsFindNextVolume() return ok. Instance=1, VolumeHandle=0x102000000
    FfsFindNextFile(file_type=5) failed. Instance=1. Next loop
    FfsFindNextVolume() enters: Instance=1
            ok. Instance=-1. BaseAddress=0x1C2040000, Length=0x460C0
    FfsFindNextVolume() return ok. Instance=2, VolumeHandle=0x1C2040000
    FfsFindNextFile(file_type=5) ok. Instance=2. Return to caller.
    add-symbol-file /home/bruin/work/tianocore/Build/MyChip/NOOPT_GCC5/AARCH64/MdeModulePkg/Core/Dxe/DxeMain/DEBUG/DxeCore.dll 0x1C1FFB000
    Loading DxeCore at 0x01C1FFA000 EntryPoint=0x01C1FFB000
    CoreInitializeMemoryServices:
      BaseAddress - 0x1BE0F1000 Length - 0x3F09000 MinimalMemorySizeNeeded - 0x34AE000
    InstallProtocolInterface: 5B1B31A1-9562-11D2-8E3F-00A0C969723B 1C203A3E0
    ProtectUefiImageCommon - 0xC203A3E0
      - 0x00000001C1FFA000 - 0x0000000000046000
    DxeMain: MemoryBaseAddress=0x1BE0F1000 MemoryLength=0x3F09000
    add-symbol-file /home/bruin/work/tianocore/Build/MyChip/NOOPT_GCC5/AARCH64/MdeModulePkg/Core/Dxe/DxeMain/DEBUG/DxeCore.dll 0x1C1FFB000
    HOBLIST address in DXE = 0x1C1A36018
    Memory Allocation 0x00000004 0x1C20E8000 - 0x1C20E8FFF
    Memory Allocation 0x00000000 0x0 - 0xFFFF
    Memory Allocation 0x00000000 0x20400000 - 0x207FFFFF
    Memory Allocation 0x00000000 0x102000000 - 0x1020BFFFF
    Memory Allocation 0x00000006 0x1020C0000 - 0x1020DFFFF
    Memory Allocation 0x00000000 0x1020E0000 - 0x1020EFFFF
    Memory Allocation 0x00000004 0x1C20E7000 - 0x1C20E7FFF
    Memory Allocation 0x00000004 0x1C20E6000 - 0x1C20E6FFF
    Memory Allocation 0x00000004 0x1C20E5000 - 0x1C20E5FFF
    Memory Allocation 0x00000004 0x1C20E4000 - 0x1C20E4FFF
    Memory Allocation 0x00000004 0x1C20E3000 - 0x1C20E3FFF
    Memory Allocation 0x00000004 0x1C20E2000 - 0x1C20E2FFF
    Memory Allocation 0x00000004 0x1C20E1000 - 0x1C20E1FFF
    Memory Allocation 0x00000004 0x1C20E0000 - 0x1C20E0FFF
    Memory Allocation 0x00000004 0x1C20E9000 - 0x1C20EFFFF
    Memory Allocation 0x00000004 0x1C20D0000 - 0x1C20DFFFF
    Memory Allocation 0x00000004 0x1C2088000 - 0x1C20CFFFF
    Memory Allocation 0x00000004 0x1C2040000 - 0x1C2087FFF
    Memory Allocation 0x00000003 0x1C1FFA000 - 0x1C203FFFF
    Memory Allocation 0x00000003 0x1C1FFA000 - 0x1C203FFFF
    FV Hob            0x102000000 - 0x1020BFFFF
    FV Hob            0x1C2040000 - 0x1C20860BF
    FV2 Hob           0x1C2040000 - 0x1C20860BF
                      56CEF77F-A38E-4B13-CF52-22A90E6FE662 - 9E21FD93-9C72-4C15-8C4B-E77F1DB2D792
    InstallProtocolInterface: D8117CFE-94A6-11D4-9A3A-0090273FC14D 1C203A390
    InstallProtocolInterface: 8F644FA9-E850-4DB1-9CE2-0B44698E8DA4 1C1A32730
    InstallProtocolInterface: 09576E91-6D3F-11D2-8E39-00A0C969723B 1C1A32298
    InstallProtocolInterface: 8F644FA9-E850-4DB1-9CE2-0B44698E8DA4 1C1A32430
    InstallProtocolInterface: 09576E91-6D3F-11D2-8E39-00A0C969723B 1C1A1E018
    InstallProtocolInterface: 220E73B6-6BDB-4413-8405-B974B108619A 1C1A1E0B0
    InstallProtocolInterface: 220E73B6-6BDB-4413-8405-B974B108619A 1C1A1E1B0
    InstallProtocolInterface: FC1BCDB0-7D31-49AA-936A-A4600D9DD083 1C203A3B0

    Security Arch Protocol not present!!

    CPU Arch Protocol not present!!

    Metronome Arch Protocol not present!!

    Timer Arch Protocol not present!!

    Bds Arch Protocol not present!!

    Watchdog Timer Arch Protocol not present!!

    Runtime Arch Protocol not present!!

    Variable Arch Protocol not present!!

    Variable Write Arch Protocol not present!!

    Capsule Arch Protocol not present!!

    Monotonic Counter Arch Protocol not present!!

    Reset Arch Protocol not present!!

    Real Time Clock Arch Protocol not present!!

    ASSERT_EFI_ERROR (Status = Not Found)
    ASSERT [DxeCore] /home/bruin/work/tianocore/edk2/MdeModulePkg/Core/Dxe/DxeMain/DxeMain.c(538): !(((INTN)(RETURN_STATUS)(Status)) < 0)
    ```

### Add other modules

- Porting customized code (ref RPi4):
    - library: `EfiResetSystemLib`
    - driver: `VarBlockServiceDxe`

- serial report (2021.11.25, commit `2013a62a`):

    ```
    add-symbol-file /home/bruin/work/tianocore/Build/MyChip/NOOPT_GCC5/AARCH64/MdeModulePkg/Core/Dxe/DxeMain/DEBUG/DxeCore.dll 0x1C1B5F000
    Loading DxeCore at 0x01C1B5E000 EntryPoint=0x01C1B5F000
    CoreInitializeMemoryServices:
      BaseAddress - 0x1BE0F1000 Length - 0x3A6D000 MinimalMemorySizeNeeded - 0x34AE000
    InstallProtocolInterface: 5B1B31A1-9562-11D2-8E3F-00A0C969723B 1C1B9E3E0
    ProtectUefiImageCommon - 0xC1B9E3E0
      - 0x00000001C1B5E000 - 0x0000000000046000
    DxeMain: MemoryBaseAddress=0x1BE0F1000 MemoryLength=0x3A6D000
    add-symbol-file /home/bruin/work/tianocore/Build/MyChip/NOOPT_GCC5/AARCH64/MdeModulePkg/Core/Dxe/DxeMain/DEBUG/DxeCore.dll 0x1C1B5F000
    HOBLIST address in DXE = 0x1C1596018
    Memory Allocation 0x00000004 0x1C20E8000 - 0x1C20E8FFF
    Memory Allocation 0x00000000 0x0 - 0xFFFF
    Memory Allocation 0x00000000 0x20400000 - 0x207FFFFF
    Memory Allocation 0x00000000 0x102000000 - 0x1020BFFFF
    Memory Allocation 0x00000006 0x1020C0000 - 0x1020DFFFF
    Memory Allocation 0x00000000 0x1020E0000 - 0x1020EFFFF
    Memory Allocation 0x00000004 0x1C20E7000 - 0x1C20E7FFF
    Memory Allocation 0x00000004 0x1C20E6000 - 0x1C20E6FFF
    Memory Allocation 0x00000004 0x1C20E5000 - 0x1C20E5FFF
    Memory Allocation 0x00000004 0x1C20E4000 - 0x1C20E4FFF
    Memory Allocation 0x00000004 0x1C20E3000 - 0x1C20E3FFF
    Memory Allocation 0x00000004 0x1C20E2000 - 0x1C20E2FFF
    Memory Allocation 0x00000004 0x1C20E1000 - 0x1C20E1FFF
    Memory Allocation 0x00000004 0x1C20E0000 - 0x1C20E0FFF
    Memory Allocation 0x00000004 0x1C20E9000 - 0x1C20EFFFF
    Memory Allocation 0x00000004 0x1C20D0000 - 0x1C20DFFFF
    Memory Allocation 0x00000004 0x1C1E3A000 - 0x1C20CFFFF
    Memory Allocation 0x00000004 0x1C1BA4000 - 0x1C1E39FFF
    Memory Allocation 0x00000003 0x1C1B5E000 - 0x1C1BA3FFF
    Memory Allocation 0x00000003 0x1C1B5E000 - 0x1C1BA3FFF
    FV Hob            0x102000000 - 0x1020BFFFF
    FV Hob            0x1C1BA4000 - 0x1C1E386BF
    FV2 Hob           0x1C1BA4000 - 0x1C1E386BF
                      56CEF77F-A38E-4B13-CF52-22A90E6FE662 - 9E21FD93-9C72-4C15-8C4B-E77F1DB2D792
    InstallProtocolInterface: D8117CFE-94A6-11D4-9A3A-0090273FC14D 1C1B9E390
    InstallProtocolInterface: 8F644FA9-E850-4DB1-9CE2-0B44698E8DA4 1C1592730
    InstallProtocolInterface: 09576E91-6D3F-11D2-8E39-00A0C969723B 1C1592298
    InstallProtocolInterface: 8F644FA9-E850-4DB1-9CE2-0B44698E8DA4 1C1592430
    InstallProtocolInterface: 09576E91-6D3F-11D2-8E39-00A0C969723B 1C14EA018
    InstallProtocolInterface: 220E73B6-6BDB-4413-8405-B974B108619A 1C14EA0B0
    InstallProtocolInterface: 220E73B6-6BDB-4413-8405-B974B108619A 1C14EA1B0
    InstallProtocolInterface: FC1BCDB0-7D31-49AA-936A-A4600D9DD083 1C1B9E3B0
    Loading driver 80CF7257-87AB-47F9-A3FE-D50B76D89541
    InstallProtocolInterface: 5B1B31A1-9562-11D2-8E3F-00A0C969723B 1C14050C0
    add-symbol-file /home/bruin/work/tianocore/Build/MyChip/NOOPT_GCC5/AARCH64/MdeModulePkg/Universal/PCD/Dxe/Pcd/DEBUG/PcdDxe.dll 0x1C1971000
    Loading driver at 0x001C1970000 EntryPoint=0x001C1971048 PcdDxe.efi
    InstallProtocolInterface: BC62157E-3E33-4FEC-9920-2D3B36D750DF 1C1405A98
    ProtectUefiImageCommon - 0xC14050C0
      - 0x00000001C1970000 - 0x0000000000010000
    InstallProtocolInterface: 11B34006-D85B-4D0A-A290-D5A571310EF7 1C197E020
    InstallProtocolInterface: 13A3F0F6-264A-3EF0-F2E0-DEC512342F34 1C197E118
    InstallProtocolInterface: 5BE40F57-FA68-4610-BBBF-E9C5FCDAD365 1C197E1A8
    InstallProtocolInterface: FD0F4478-0EFD-461D-BA2D-E58C45FD5F5E 1C197E1C0
    Loading driver B601F8C4-43B7-4784-95B1-F4226CB40CEE
    InstallProtocolInterface: 5B1B31A1-9562-11D2-8E3F-00A0C969723B 1C1402240
    add-symbol-file /home/bruin/work/tianocore/Build/MyChip/NOOPT_GCC5/AARCH64/MdeModulePkg/Core/RuntimeDxe/RuntimeDxe/DEBUG/RuntimeDxe.dll 0x1C19D0000
    Loading driver at 0x001C19C0000 EntryPoint=0x001C19D0048 RuntimeDxe.efi
    InstallProtocolInterface: BC62157E-3E33-4FEC-9920-2D3B36D750DF 1C1402798
    ProtectUefiImageCommon - 0xC1402240
      - 0x00000001C19C0000 - 0x0000000000040000
    InstallProtocolInterface: B7DFB4E1-052F-449F-87BE-9818FC91B733 1C19E0008
    Loading driver F80697E9-7FD6-4665-8646-88E33EF71DFC
    InstallProtocolInterface: 5B1B31A1-9562-11D2-8E3F-00A0C969723B 1C1401040
    add-symbol-file /home/bruin/work/tianocore/Build/MyChip/NOOPT_GCC5/AARCH64/MdeModulePkg/Universal/SecurityStubDxe/SecurityStubDxe/DEBUG/SecurityStubDxe.dll 0x1C1961000
    Loading driver at 0x001C1960000 EntryPoint=0x001C1961048 SecurityStubDxe.efi
    InstallProtocolInterface: BC62157E-3E33-4FEC-9920-2D3B36D750DF 1C1401D98
    ProtectUefiImageCommon - 0xC1401040
      - 0x00000001C1960000 - 0x0000000000010000
    InstallProtocolInterface: 94AB2F58-1438-4EF1-9152-18941A3A0E68 1C196E010
    InstallProtocolInterface: A46423E3-4617-49F1-B9FF-D1BFA9115839 1C196E008
    InstallProtocolInterface: 15853D7C-3DDF-43E0-A1CB-EBF85B8F872C 1C196E018
    Loading driver 733CBAC2-B23F-4B92-BC8E-FB01CE5907B7
    InstallProtocolInterface: 5B1B31A1-9562-11D2-8E3F-00A0C969723B 1C1401540
    add-symbol-file /home/bruin/work/tianocore/Build/MyChip/NOOPT_GCC5/AARCH64/Platform/MyCorp/MyChip/Drivers/VarBlockServiceDxe/VarBlockServiceDxe/DEBUG/VarBlockServiceDxe.dll 0x1BE660000
    Loading driver at 0x001BE650000 EntryPoint=0x001BE660048 VarBlockServiceDxe.efi
    InstallProtocolInterface: BC62157E-3E33-4FEC-9920-2D3B36D750DF 1C121AB18
    ProtectUefiImageCommon - 0xC1401540
      - 0x00000001BE650000 - 0x0000000000040000
    InstallProtocolInterface: 8F644FA9-E850-4DB1-9CE2-0B44698E8DA4 1C1B3F9A0
    InstallProtocolInterface: 09576E91-6D3F-11D2-8E39-00A0C969723B 1C121AD98
    Loading driver CBD2E4D5-7068-4FF5-B462-9822B4AD8D60
    InstallProtocolInterface: 5B1B31A1-9562-11D2-8E3F-00A0C969723B 1C121A240
    add-symbol-file /home/bruin/work/tianocore/Build/MyChip/NOOPT_GCC5/AARCH64/MdeModulePkg/Universal/Variable/RuntimeDxe/VariableRuntimeDxe/DEBUG/VariableRuntimeDxe.dll 0x1BE600000
    Loading driver at 0x001BE5F0000 EntryPoint=0x001BE600048 VariableRuntimeDxe.efi
    InstallProtocolInterface: BC62157E-3E33-4FEC-9920-2D3B36D750DF 1C125BF98
    ProtectUefiImageCommon - 0xC121A240
      - 0x00000001BE5F0000 - 0x0000000000050000


    Synchronous Exception at 0x00000001BE60C238
    PC 0x0001BE60C238 (0x0001BE5F0000+0x0001C238) [ 0] VariableRuntimeDxe.dll
    PC 0x0001BE60BF40 (0x0001BE5F0000+0x0001BF40) [ 0] VariableRuntimeDxe.dll
    PC 0x0001BE609518 (0x0001BE5F0000+0x00019518) [ 0] VariableRuntimeDxe.dll
    PC 0x0001BE609AF4 (0x0001BE5F0000+0x00019AF4) [ 0] VariableRuntimeDxe.dll
    PC 0x0001BE608C78 (0x0001BE5F0000+0x00018C78) [ 0] VariableRuntimeDxe.dll
    PC 0x0001BE6010EC (0x0001BE5F0000+0x000110EC) [ 0] VariableRuntimeDxe.dll
    PC 0x0001BE600630 (0x0001BE5F0000+0x00010630) [ 0] VariableRuntimeDxe.dll
    PC 0x0001BE600168 (0x0001BE5F0000+0x00010168) [ 0] VariableRuntimeDxe.dll
    PC 0x0001C1B64CA4 (0x0001C1B5E000+0x00006CA4) [ 1] DxeCore.dll
    PC 0x0001C1B81FC0 (0x0001C1B5E000+0x00023FC0) [ 1] DxeCore.dll
    PC 0x0001C1B601A0 (0x0001C1B5E000+0x000021A0) [ 1] DxeCore.dll
    PC 0x0001C1B5F36C (0x0001C1B5E000+0x0000136C) [ 1] DxeCore.dll
    PC 0x0001C1B5F024 (0x0001C1B5E000+0x00001024) [ 1] DxeCore.dll
    PC 0x0001020056D8
    PC 0x0001020058B0
    PC 0x000102000A1C
    PC 0x000102000BB8
    PC 0x000102000B54

    [ 0] /home/bruin/work/tianocore/Build/MyChip/NOOPT_GCC5/AARCH64/MdeModulePkg/Universal/Variable/RuntimeDxe/VariableRuntimeDxe/DEBUG/VariableRuntimeDxe.dll
    [ 1] /home/bruin/work/tianocore/Build/MyChip/NOOPT_GCC5/AARCH64/MdeModulePkg/Core/Dxe/DxeMain/DEBUG/DxeCore.dll

      X0 0x00000001C1A30018   X1 0x00000000000C0000   X2 0x000000000000E000   X3 0x00000001C1A30010
      X4 0x00000000000CE000   X5 0x00000001C1A3E018   X6 0x00000001BE60D338   X7 0x0000000000000000
      X8 0x00000001C1B5DE08   X9 0x0000000000000008  X10 0x00000001C1A30000  X11 0x00000001C1B3FFFF
    X12 0x0000000000000000  X13 0x000000000000000E  X14 0x00000001C1B37598  X15 0x00000001C1B3E998
    X16 0x00000001C20EFBF0  X17 0x0000000000000000  X18 0x0000000000000000  X19 0x0000000000000000
    X20 0x0000000000000000  X21 0x0000000000000000  X22 0x0000000000000000  X23 0x00000001C20E9000
    X24 0x0000000081000000  X25 0x0000000000004000  X26 0x0000000000001000  X27 0x00000001020002D8
    X28 0x0000000000000000   FP 0x00000001C20EFA30   LR 0x00000001BE60BF40

      V0 0x0000000000000000 0000000000000000   V1 0x0000000000000000 0000000000000000
      V2 0x0000000000000000 0000000000000000   V3 0x0000000000000000 0000000000000000
      V4 0x0000000000000000 0000000000000000   V5 0x0000000000000000 0000000000000000
      V6 0x0000000000000000 0000000000000000   V7 0x0000000000000000 0000000000000000
      V8 0x0000000000000000 0000000000000000   V9 0x0000000000000000 0000000000000000
    V10 0x0000000000000000 0000000000000000  V11 0x0000000000000000 0000000000000000
    V12 0x0000000000000000 0000000000000000  V13 0x0000000000000000 0000000000000000
    V14 0x0000000000000000 0000000000000000  V15 0x0000000000000000 0000000000000000
    V16 0x0000000000000000 0000000000000000  V17 0x0000000000000000 0000000000000000
    V18 0x0000000000000000 0000000000000000  V19 0x0000000000000000 0000000000000000
    V20 0x0000000000000000 0000000000000000  V21 0x0000000000000000 0000000000000000
    V22 0x0000000000000000 0000000000000000  V23 0x0000000000000000 0000000000000000
    V24 0x0000000000000000 0000000000000000  V25 0x0000000000000000 0000000000000000
    V26 0x0000000000000000 0000000000000000  V27 0x0000000000000000 0000000000000000
    V28 0x0000000000000000 0000000000000000  V29 0x0000000000000000 0000000000000000
    V30 0x0000000000000000 0000000000000000  V31 0x0000000000000000 0000000000000000

      SP 0x00000001C20EFA30  ELR 0x00000001BE60C238  SPSR 0x200003C5  FPSR 0x00000000
    ESR 0x96000007          FAR 0x00000000000C0000

    ESR : EC 0x25  IL 0x1  ISS 0x00000007

    Data abort: Translation fault, third level

    Stack dump:
      00001C20EF930: 00000001C20EF980 0000000000000004 00000001C20EF970 0000000000000010
      00001C20EF950: 00000001C20EF980 00000001C19736DC 0000000000000003 00000001C197E008
      00001C20EF970: 00000001C20EF9A0 0000000000000004 00000001C20EF9B0 00000001C1976CF0
      00001C20EF990: 0000000000000008 00000001C140557E 00000001C20EF9B0 00000001C1B6DB1C
      00001C20EF9B0: 0000000000000020 0000000000000000 00000001C20EF9E0 00000001C1976D7C
      00001C20EF9D0: 0000000000000020 0000000000000000 00000001C20EFA20 00000001C1971A74
      00001C20EF9F0: 0000000000000000 0000000000000003 00000001C1405578 00000001C1405578
      00001C20EFA10: 00000001C14055FC 000C000000000000 00000001C20EFA40 00000001BE60BA70
    > 00001C20EFA30: 00000001C20EFA60 00000001BE609518 00000001C20EFA60 000000000000E000
      00001C20EFA50: 00000000000C0000 00000001C1A30018 00000001C20EFAE0 00000001BE609AF4
      00001C20EFA70: 0000000000000000 00000001C20EFB08 0000000000000040 00000001C20EFAD0
      00001C20EFA90: 0000000000000108 00000006C1B3E898 00000001C20EFAE0 0000000000000000
      00001C20EFAB0: 00000001C20EFAE0 00000001BE60D3B4 00000001C20EFAE0 00000000000C0000
      00001C20EFAD0: 00000001C1A30018 0000E000C1B3D998 00000001C20EFB30 00000001BE608C78
      00001C20EFAF0: 0000000000000000 00000001BE600680 0000000000000010 00000001C1B3D9F8
      00001C20EFB10: 00000001C20EFB30 00000001BE608C74 0000000000000010 00000001C1B3D9F8
    ASSERT [DxeCore] /home/bruin/work/tianocore/edk2/ArmPkg/Library/DefaultExceptionHandlerLib/AArch64/DefaultExceptionHandler.c(273): ((BOOLEAN)(0==1))
    ```

    So it seems that `VariableRuntimeDxe` module aborted. The entry point of the module `VariableServiceInitialize()` can be found in the "Execution Order Prediction" section of the build-report. If just return `EFI_SUCCESS` in `VariableServiceInitialize()`, DXE Core will continue load other drivers until it complains some protocols are not found (see below). So it seems that something wrong with `VariableRuntimeDxe` module (probably just some Pcd values?).

    ```
    Loading driver at 0x001C1934000 EntryPoint=0x001C1935048 FaultTolerantWriteDxe.efi
    InstallProtocolInterface: BC62157E-3E33-4FEC-9920-2D3B36D750DF 1C140D318
    ProtectUefiImageCommon - 0xC140D0C0
      - 0x00000001C1934000 - 0x000000000000F000
    Ftw: FtwWorkSpaceLba - 0xF, WorkBlockSize  - 0x1000, FtwWorkSpaceBase - 0x0
    Ftw: FtwSpareLba     - 0x10, SpareBlockSize - 0x1000
    Ftw: NumberOfWorkBlock - 0x1, FtwWorkBlockLba - 0xF
    Ftw: WorkSpaceLbaInSpare - 0x0, WorkSpaceBaseInSpare - 0x0
    Ftw: Remaining work space size - FE0
    InstallProtocolInterface: 3EBD9E82-2C78-4DE6-9786-8D4BFCB7C881 1C140B028

    CPU Arch Protocol not present!!

    Timer Arch Protocol not present!!

    Bds Arch Protocol not present!!

    Watchdog Timer Arch Protocol not present!!

    Variable Arch Protocol not present!!

    Variable Write Arch Protocol not present!!

    Capsule Arch Protocol not present!!

    Monotonic Counter Arch Protocol not present!!

    Real Time Clock Arch Protocol not present!!
    Driver B8D9777E-D72A-451F-9BDB-BAFB52A68415 was discovered but not loaded!!
    Driver 42857F0A-13F2-4B21-8A23-53D3F714B840 was discovered but not loaded!!
    Driver AD608272-D07F-4964-801E-7BD3B7888652 was discovered but not loaded!!
    Driver B336F62D-4135-4A55-AE4E-4971BBF0885D was discovered but not loaded!!

    ASSERT_EFI_ERROR (Status = Not Found)
    ASSERT [DxeCore] /home/bruin/work/tianocore/edk2/MdeModulePkg/Core/Dxe/DxeMain/DxeMain.c(538): !(((INTN)(RETURN_STATUS)(Status)) < 0)
    ```
- `DxeMain()` call sequence anaysis:

```
DxeMain()          <= MdeModulePkg/Core/Dxe/DxeMain/DxeMain.c
|-- InitializeCpuExceptionHandlersEx()
|-- InitializeDebugAgent()
|-- CoreInitializeMemoryServices()
|   |-- ...
|   |-- DEBUG("CoreInitializeMemoryServices:\n");
|   |-- DEBUG("  BaseAddress - 0x%lx Length - 0x%lx MinimalMemorySizeNeeded - 0x%lx\n");
|   `-- ...
|-- MemoryProfileInit()
|-- AllocateRuntimeCopyPool(EFI_SYSTEM_TABLE)
|-- AllocateRuntimeCopyPool(EFI_RUNTIME_SERVICES)
|-- CoreInitializeImageServices()
|   |-- ...
|   |-- CoreInstallProtocolInterface()
|   |   `-- CoreInstallProtocolInterfaceNotify()
|   |       |-- DEBUG("InstallProtocolInterface: %g %p\n", Protocol, Interface))
|   |       |-- ...
|   `-- ProtectUefiImage()
|       |-- DEBUG("ProtectUefiImageCommon - 0x%x\n", LoadedImage)
|       |-- DEBUG("  - 0x%016lx - 0x%016lx\n", ImageBase, ImageSize)
|       |-- ...
|-- CoreInitializeGcdServices()
|-- ProcessLibraryConstructorList()
|-- DEBUG("DxeMain: MemoryBaseAddress=0x1BE0F1000 MemoryLength=0x3A8D000")
|-- PeCoffLoaderGetEntryPoint()
|-- PeCoffLoaderRelocateImageExtraAction()
|   `-- DEBUG("add-symbol-file %a 0x%p\n",...);
|-- CoreInstallConfigurationTable(gEfiDxeServicesTableGuid,...)
|-- CoreInstallConfigurationTable(gEfiHobListGuid,...)
|-- CoreInstallConfigurationTable(gEfiMemoryTypeInformationGuid,...)
|-- CoreInitializeDebugImageInfoTable()
|-- CoreNewDebugImageInfoEntry()
|-- DEBUG("HOBLIST address in DXE = 0x%p\n")
|-- DEBUG("Memory Allocation 0x%08x 0x%0lx - 0x%0lx\n", mem_type, start_addr, end_addr)
|-- DEBUG("FV Hob   0x%0lx 0x%0lx", start_addr, end_addr)
|-- DEBUG("FV2 Hob   0x%0lx 0x%0lx", start_addr, end_addr)
|-- CoreInitializeEventServices()
|   |-- InitializeListHead (&gEventQueue[0:31]);
|   |-- CoreInitializeTimer()
|   |   `-- CoreCreateEventInternal(..., CoreCheckTimers, mEfiCheckTimerEvent)
|   `-- CoreCreateEventEx(..., EfiEventEmptyFunction,...,&gIdleLoopEventGuid, &gIdleLoopEvent)
|-- MemoryProfileInstallProtocol()
|-- CoreInitializeMemoryAttributesTable()
|-- CoreInitializeMemoryProtection()
|-- GetNextGuidHob (&gEfiVectorHandoffInfoPpiGuid,...)
|-- CoreInstallConfigurationTable(&gEfiVectorHandoffInfoPpiGuid,...)
|-- CoreInstallMultipleProtocolInterfaces(&mDecompressHandle,...)
|-- CoreNotifyOnProtocolInstallation()
|   |-- CoreNotifyOnProtocolEntryTable (mArchProtocols[])
|   |   |-- CoreCreateEvent(EVT_NOTIFY_SIGNAL, GenericProtocolNotify,...)
|   |   `-- CoreRegisterProtocolNotify()
|   `-- CoreNotifyOnProtocolEntryTable (mOptionalProtocols[])
|-- FwVolBlockDriverInit()
|-- FwVolDriverInit()
|-- InitializeSectionExtraction()
|-- CoreInitializeDispatcher()
|-- CoreDispatcher()
|   |-- ...
|-- CoreDisplayMissingArchProtocols()
|-- CoreDisplayDiscoveredNotDispatched()
|-- CoreAllEfiServicesAvailable()
`--   gBds->Entry(gBds);
```

The debug info shows that the missing AP (Archtectural Protocols) are (w/ corresponding drivers in RPi4):

- Timer: edk2/ArmPkg/Drivers/TimerDxe/TimerDxe.inf
- CPU: edk2/ArmPkg/Drivers/CpuDxe/CpuDxe.inf
- Watchdog Timer: edk2/MdeModulePkg/Universal/WatchdogTimerDxe/WatchdogTimer.inf
- Variable: edk2/MdeModulePkg/Universal/Variable/RuntimeDxe/VariableRuntimeDxe.inf
- Variable Write: ditto
- Capsule: edk2/MdeModulePkg/Universal/CapsuleRuntimeDxe/CapsuleRuntimeDxe.inf
- Monotonic Counter: edk2/MdeModulePkg/Universal/MonotonicCounterRuntimeDxe/MonotonicCounterRuntimeDxe.inf
- Real Time Clock: edk2/EmbeddedPkg/RealTimeClockRuntimeDxe/RealTimeClockRuntimeDxe.inf
- Bds: edk2/MdeModulePkg/Universal/BdsDxe/BdsDxe.inf

The full list of required APs are in `DxeProtocolNotify.c`:

```
EFI_CORE_PROTOCOL_NOTIFY_ENTRY  mArchProtocols[] = {
  { &gEfiSecurityArchProtocolGuid,         (VOID **)&gSecurity,      NULL, NULL, FALSE },
  { &gEfiCpuArchProtocolGuid,              (VOID **)&gCpu,           NULL, NULL, FALSE },
  { &gEfiMetronomeArchProtocolGuid,        (VOID **)&gMetronome,     NULL, NULL, FALSE },
  { &gEfiTimerArchProtocolGuid,            (VOID **)&gTimer,         NULL, NULL, FALSE },
  { &gEfiBdsArchProtocolGuid,              (VOID **)&gBds,           NULL, NULL, FALSE },
  { &gEfiWatchdogTimerArchProtocolGuid,    (VOID **)&gWatchdogTimer, NULL, NULL, FALSE },
  { &gEfiRuntimeArchProtocolGuid,          (VOID **)&gRuntime,       NULL, NULL, FALSE },
  { &gEfiVariableArchProtocolGuid,         (VOID **)NULL,            NULL, NULL, FALSE },
  { &gEfiVariableWriteArchProtocolGuid,    (VOID **)NULL,            NULL, NULL, FALSE },
  { &gEfiCapsuleArchProtocolGuid,          (VOID **)NULL,            NULL, NULL, FALSE },
  { &gEfiMonotonicCounterArchProtocolGuid, (VOID **)NULL,            NULL, NULL, FALSE },
  { &gEfiResetArchProtocolGuid,            (VOID **)NULL,            NULL, NULL, FALSE },
  { &gEfiRealTimeClockArchProtocolGuid,    (VOID **)NULL,            NULL, NULL, FALSE },
  { NULL,                                  (VOID **)NULL,            NULL, NULL, FALSE }
};
```

`CoreDispatcher()` call sequence:

```
|-- CoreInitializeDispatcher()
|   `-- EfiCreateProtocolNotifyEvent(&gEfiFirmwareVolume2ProtocolGuid,...)
|       |-- gBS->CreateEvent(EVT_NOTIFY_SIGNAL)
|       |-- gBS->RegisterProtocolNotify()
|       `-- gBS->SignalEvent()
|-- CoreDispatcher()
    |-- CoreCreateEventEx(EVT_NOTIFY_SIGNAL, ..., &gEfiEventDxeDispatchGuid,...)
    |-- for each driver in mScheduledQueue
    |   |-- DriverEntry = CR()
    |   |-- DEBUG("Loading driver %g\n")
    |   |-- CoreLoadImage()
    |   |   `-- CoreLoadImageCommon()
    |   |       |-- ...
    |   |       |-- CoreInstallProtocolInterfaceNotify(EFI_LOADED_IMAGE_PROTOCOL_GUID) # w/o notify
    |   |       |   |-- DEBUG("InstallProtocolInterface: %g %p\n", protocol, if))
    |   |       |   |-- ...
    |   |       |-- CoreLoadPeImage()
    |   |       |   |-- ...
    |   |       |   |-- PeCoffLoaderRelocateImage()
    |   |       |   |   |-- PeCoffLoaderRelocateImageExtraAction()
    |   |       |   |   |   `-- DEBUG("add-symbol-file %a 0x%p\n",... )
    |   |       |   |   |-- ...
    |   |       |   |-- DEBUG("Loading driver at 0x%11p EntryPoint=0x%11p ")
    |   |       |   |-- ...
    |   |       |-- CoreReinstallProtocolInterface(EFI_LOADED_IMAGE_PROTOCOL_GUID) # w/ notify
    |   |       |   |-- CoreFindProtocolInterface(hdl, proto, if)
    |   |       |   |-- CoreDisconnectControllersUsingProtocolInterface()
    |   |       |   |-- CoreRemoveInterfaceFromProtocol()
    |   |       |   |-- InsertTailList()
    |   |       |   |-- CoreConnectController()
    |   |       |   `-- CoreNotifyProtocolEntry()
    |   |       |-- CoreInstallProtocolInterface(EFI_LOADED_IMAGE_DEVICE_PATH_PROTOCOL_GUID)
    |   |       |   `-- CoreInstallProtocolInterfaceNotify(EFI_LOADED_IMAGE_DEVICE_PATH_PROTOCOL_GUID)
    |   |       |       |-- DEBUG("InstallProtocolInterface: %g %p\n", protocol, if))
    |   |       |       |-- ...
    |   |       |-- CoreInstallProtocolInterface(EFI_HII_PACKAGE_LIST_PROTOCOL_GUID)
    |   |       `-- ProtectUefiImage(interface, device_path)
    |   |           |-- DEBUG("ProtectUefiImageCommon - 0x%x\n", interface);
    |   |           |-- DEBUG("  - 0x%016lx - 0x%016lx\n", ImageBase, ImageSize))
    |   |           |-- ...
    |   `-- CoreStartImage(handle)
    |       |-- ...
    |       |-- Image->EntryPoint (ImageHandle, Image->Info.SystemTable)
    |       |-- ...
    `-- CoreCloseEvent()
```

### VariableRunTimeDxe bug

Using the call stack info, and `objdump -S VariableRuntimeDxe.dll`, it seems the exception is caused by `InitRealNonVolatileVariableStore()->CopyMem(NvStorageData, NvStorageBase, NvStorageSize)`, where `NvStorageBase` was `0xc0000`, but the real value should be `0x1020c0000`. After hard-coding the value to `0x1020c0000`, the exception disapears. there are following questions to be resolved:

- why the `DEBUG((DEBUG_INFO,...))` within `InitRealNonVolatileVariableStore()` is not printed? By tracing the `DEBUG()` call, togther with `objdump -S VariableRuntimeDxe.dll`, and examing ` VariableRuntimeDxe.map`, the function `DebugPrintEnabled()` is coming from `MdePkg/Library/BaseDebugLibNull/BaseDebugLibNull.inf`! Why is that? this is because it's specified in the DSC for `VariableRuntimeDxe.inf`. After removing that line from DSC, the `BaseDebugLibSerialPort.inf` (`DebugLib` instance) is chosen, and debug print is ok!
- why `PcdGet64(PcdFlashNvStorageVariableBase64)=0xC0000` (should be `0x1020c0000`)? How dynamic PCD works? `gEfiMdeModulePkgTokenSpaceGuid.PcdFlashNvStorageVariableBase64` is a dynamic pcd (`[PcdsDynamicDefault]`), how the value is set before get?
    - The workaround is to make a copy of edk2's VariableRuntimeDxe driver, and add a fixed Pcd for the base value. Not using `NV_STORAGE_VARIABLE_BASE`. commit 'ba53f6a' on 2021-11-30.
- how edk2 produces the call stack? walk the stack?
- what's the reason for `driver discovered but not loaded`: because of DEPEX evaluated to FALSE.

    ```
    CPU Arch Protocol not present!!
    Timer Arch Protocol not present!!
    Bds Arch Protocol not present!!
    Watchdog Timer Arch Protocol not present!!
    Variable Write Arch Protocol not present!!
    Capsule Arch Protocol not present!!
    Monotonic Counter Arch Protocol not present!!

    Driver B8D9777E-D72A-451F-9BDB-BAFB52A68415 was discovered but not loaded!!  <= ArmCpuDxe
    Driver 42857F0A-13F2-4B21-8A23-53D3F714B840 was discovered but not loaded!!  <= CapsuleRuntimeDxe
    Driver AD608272-D07F-4964-801E-7BD3B7888652 was discovered but not loaded!!  <= MonotonicCounterRuntimeDxe
    Driver 49EA041E-6752-42CA-B0B1-7344FE2546B7 was discovered but not loaded!!  <= ArmTimerDxe
    Driver F099D67F-71AE-4C36-B2A3-DCEB0EB2B7D8 was discovered but not loaded!!  <= WatchdogTimer
    ```

`VariableRuntimeDxe` call sequence:

```
VariableServiceInitialize()
`-- VariableCommonInitialize()
    `-- InitNonVolatileVariableStore()
        `-- InitRealNonVolatileVariableStore()
            `-- CopyMem()
```

### Timer INTID bug

- it seems that RPI4B is GICv2: https://forums.raspberrypi.com/viewtopic.php?t=244479&start=25
- on FPGA, `ArmGicGetSupportedArchRevision()=ARM_GIC_ARCH_REVISION_3`. `ArmGicGetSupportedArchRevision()` is defined in `ArmPkg/Library/ArmGicArchSecLib/ArmGicArchLib.c`.

- When start `ArmTimerDxe.efi`, recursive exception occured (`0x1658` in `ArmCpuDxe.dll` is   `CpuEnableInterrupt()`):

    ```
    _ModuleEntryPoint() enters...
    TimerInitialize() enters...
    TimerInitialize(): PcdArmArchTimerVirtIntrNum=27 done!
    TimerInitialize(): TimerHypIntrNum=26 done!
    TimerInitialize(): about to register PcdArmArchTimerIntrNum=30...

    Synchronous Exception at 0x00000001C18DA284
    PC 0x0001C18DA284 (0x0001C18D5000+0x00005284) [ 0] ArmCpuDxe.dll
    PC 0x0001C18D6658 (0x0001C18D5000+0x00001658) [ 0] ArmCpuDxe.dll
    PC 0x0001C1B46474 (0x0001C1B24000+0x00022474) [ 1] DxeCore.dll
    PC 0x0001C1B46780 (0x0001C1B24000+0x00022780) [ 1] DxeCore.dll
    PC 0x0001C18BE76C (0x0001C18BD000+0x0000176C) [ 2] ArmTimerDxe.dll
    PC 0x0001C18E9028 (0x0001C18E7000+0x00002028) [ 3] ArmGicDxe.dll
    PC 0x0001C18D9B78 (0x0001C18D5000+0x00004B78) [ 4] ArmCpuDxe.dll
    PC 0x0001C18D9CEC (0x0001C18D5000+0x00004CEC) [ 4] ArmCpuDxe.dll
    PC 0x0001C1B46474 (0x0001C1B24000+0x00022474) [ 5] DxeCore.dll
    PC 0x0001C1B46780 (0x0001C1B24000+0x00022780) [ 5] DxeCore.dll
    ...
    PC 0x0001C18BE76C (0x0001C18BD000+0x0000176C) [ 234] ArmTimerDxe.dll
    PC 0x0001C18E9028 (0x0001C18E7000+0x00002028) [ 235] ArmGicDxe.dll
    PC 0x0001C18D9B78 (0x0001C18D5000+0x00004B78) [ 236] ArmCpuDxe.dll
    PC 0x0001C18D9CEC (0x0001C18D5000+0x00004CEC) [ 236] ArmCpuDxe.dll
    PC 0x0001C18BE430 (0x0001C18BD000+0x00001430) [ 237] ArmTimerDxe.dll
    PC 0x0001C18BE19C (0x0001C18BD000+0x0000119C) [ 237] ArmTimerDxe.dll
    PC 0x0001C1B2AD4C (0x0001C1B24000+0x00006D4C) [ 238] DxeCore.dll
    PC 0x0001C1B48068 (0x0001C1B24000+0x00024068) [ 238] DxeCore.dll
    PC 0x0001C1B261A0 (0x0001C1B24000+0x000021A0) [ 238] DxeCore.dll
    ```

    If disable `CpuEnableInterrupt()` (by disable the call to `ArmEnableInterrupts()`), then the exception disappears.
- what's the interaction among Timer/Gic/Cpu/DxeCore modules?

```
       (7)                          (8)
        ^                            ^
        |                            |
+---------------+            +---------------+
|  ArmCpuDxe    |            |  ArmTimerDxe  |
+---------------+            +---------------+
   ^        ^                   ^        ^
   |        |                   |        |
   |        +-------------->----+        |
   |        |                            |     (1): gPcdProtocolGuid
   |       (5)    (6)                    |     (2): gEfiPcdProtocolGuid
   |        ^      ^                     |     (3): gGetPcdInfoProtocolGuid
   |        |      |                     |     (4): gEfiGetPcdInfoProtocolGuid
   |    +---------------+                |     (5): gHardwareInterruptProtocolGuid
   |    |  ArmGicDxe    |                |     (6): gHardwareInterrupt2ProtocolGuid
   |    +---------------+                |     (7): gEfiCpuArchProtocolGuid
   |          ^                          |     (8): gEfiTimerArchProtocolGuid
   |          |                          |
   +----<-----+------------->------------+
              |
         (1) (2) (3) (4)
          ^   ^   ^   ^
          |   |   |   |
        +---------------+
        |    PcdDxe     |
        +---------------+
```


Notes:

- Protocols produced/consumed above:
    - (1): 11B34006-D85B-4D0A-A290-D5A571310EF7, gPcdProtocolGuid
    - (2): 13A3F0F6-264A-3EF0-F2E0-DEC512342F34, gEfiPcdProtocolGuid
    - (3): 5BE40F57-FA68-4610-BBBF-E9C5FCDAD365, gGetPcdInfoProtocolGuid
    - (4): FD0F4478-0EFD-461D-BA2D-E58C45FD5F5E, gEfiGetPcdInfoProtocolGuid
    - (5): 2890B3EA-053D-1643-AD0C-D64808DA3FF1, gHardwareInterruptProtocolGuid

        ```
        struct _EFI_HARDWARE_INTERRUPT_PROTOCOL {
          HARDWARE_INTERRUPT_REGISTER         RegisterInterruptSource;
          HARDWARE_INTERRUPT_ENABLE           EnableInterruptSource;
          HARDWARE_INTERRUPT_DISABLE          DisableInterruptSource;
          HARDWARE_INTERRUPT_INTERRUPT_STATE  GetInterruptSourceState;
          HARDWARE_INTERRUPT_END_OF_INTERRUPT EndOfInterrupt;
        };
        ```

    - (6): 32898322-2DA1-474A-BAAA-F3F7CF569470, gHardwareInterrupt2ProtocolGuid

        ```
        struct _EFI_HARDWARE_INTERRUPT2_PROTOCOL {
          HARDWARE_INTERRUPT2_REGISTER            RegisterInterruptSource;
          HARDWARE_INTERRUPT2_ENABLE              EnableInterruptSource;
          HARDWARE_INTERRUPT2_DISABLE             DisableInterruptSource;
          HARDWARE_INTERRUPT2_INTERRUPT_STATE     GetInterruptSourceState;
          HARDWARE_INTERRUPT2_END_OF_INTERRUPT    EndOfInterrupt;
          // v2 members
          HARDWARE_INTERRUPT2_GET_TRIGGER_TYPE    GetTriggerType;
          HARDWARE_INTERRUPT2_SET_TRIGGER_TYPE    SetTriggerType;
        };
        ```

    - (7): 26BACCB1-6F42-11D4-BCE7-0080C73C8881, gEfiCpuArchProtocolGuid

        ```
        struct _EFI_CPU_ARCH_PROTOCOL {
          EFI_CPU_FLUSH_DATA_CACHE            FlushDataCache;
          EFI_CPU_ENABLE_INTERRUPT            EnableInterrupt;
          EFI_CPU_DISABLE_INTERRUPT           DisableInterrupt;
          EFI_CPU_GET_INTERRUPT_STATE         GetInterruptState;
          EFI_CPU_INIT                        Init;
          EFI_CPU_REGISTER_INTERRUPT_HANDLER  RegisterInterruptHandler;
          EFI_CPU_GET_TIMER_VALUE             GetTimerValue;
          EFI_CPU_SET_MEMORY_ATTRIBUTES       SetMemoryAttributes;
          UINT32                              NumberOfTimers;
          UINT32                              DmaBufferAlignment;
        };
        ```

    - (8): 26BACCB3-6F42-11D4-BCE7-0080C73C8881, gEfiTimerArchProtocolGuid

        ```
        struct _EFI_TIMER_ARCH_PROTOCOL {
          EFI_TIMER_REGISTER_HANDLER          RegisterHandler;
          EFI_TIMER_SET_TIMER_PERIOD          SetTimerPeriod;
          EFI_TIMER_GET_TIMER_PERIOD          GetTimerPeriod;
          EFI_TIMER_GENERATE_SOFT_INTERRUPT   GenerateSoftInterrupt;
        };
        ```

- Difference between (1) and (2): the latter is only for accessing Dynamic-Ex type PCD, as defined in PI v1.2 Vol3.
- Difference between (5) and (6): the latter added two methods to get/set trigger type
- Sequence to install the timer handler:
    - `ArmTimerDxe` installs (8)
    - `DxeCore` gets notified on (8)'s intallation, since, for each DxeCore interested protocol:
        - DxeCore creates a SIGNAL event with `GenericProtocolNotify()` callback.
        - DxeCore registers the event via `CoreRegisterProtocolNotify(proto, event)`.
    - `DxeCore` registers the periodic timer handler `CoreTimerTick` from within the callback `GenericProtocolNotify()` if the protocol matches `gEfiTimerArchProtocolGuid`, via `gTimer->RegisterHandler (gTimer, CoreTimerTick)`.
    - Periodically, `CoreTimerTick()` signals `mEfiCheckTimerEvent`, causing `CoreCheckTimers()` to be called.


| Id | Handler                  | Module          |      Registered              |    Triggered             |
|---:|:-------------------------|:----------------|:-----------------------------|:-------------------------|
| A  | `CoreCheckTimers()`      | DxeCore         | to `mEfiCheckTimerEvent`     | B signals `mEfiCheckTimerEvent` |
| B  | `CoreTimerTick()`        | DxeCore         | on `GenericProtocolNotify()`, via `gTimer->RegisterHandler(gTimer, B)`: B assigned to `mTimerNotifyFunction` | C calls B |
| C  | `TimerInterruptHandler()`| ArmTimerDxe     | via `gInterrupt->RegisterInterruptSource(INTID, C)` for 4 INTIDs: C assigned to `gRegisteredInterruptHandlers[INTID]` | D calls C |
| D  |`GicV3IrqInterruptHandler()`| ArmGicDxe     | on `CpuArchEventProtocolNotify()`, via `Cpu->RegisterInterruptHandler(IRQ, D)` | E calls D |
| E  | `CommonCExceptionHandler()` | ArmCpuDxe<br>(ArmExceptionLib) | called via `CommonExceptionEntry` in `ExceptionSupport.S` |


Add debug trace in `ArmGicV3Dxe.c:GicV3DxeInitialize()`, we got the following log:

```
Loading driver at 0x001C18E7000 EntryPoint=0x001C18E8048 ArmGicDxe.efi
InstallProtocolInterface: BC62157E-3E33-4FEC-9920-2D3B36D750DF 1C1200998
ProtectUefiImageCommon - 0xC1200140
  - 0x00000001C18E7000 - 0x000000000000B000
CoreStartImage(): Image->EntryPoint=0x1C18E8048
_ModuleEntryPoint() enters...
GicV3DxeInitialize(): CurrentEL=1                                   <= EL1
GicV3DxeInitialize(): mGicDistributorBase=0x20100000                <= GICD Base
GicV3DxeInitialize(): mGicRedistributorsBase=0x20140000             <= GICR Base
GicV3DxeInitialize(): mGicNumInterrupts=64
ArmGicSetInterruptPriority(): Source=0, Priority=128
ArmGicSetInterruptPriority(): Source=1, Priority=128
...
ArmGicSetInterruptPriority(): Source=63, Priority=128
GicV3DxeInitialize(): MpId=0x81000000, CpuTarget=0x0
GicV3DxeInitialize(): ICC_CTLR_EL1=0x8400; ICC_CTLR_EL1.EOImode=0   <= EOImode
```

As `EOImode=0`, the end of an interrupt can be done by a single step (i.e., write source `INITD` to `ICC_EOIR1_EL1`), via `ArmGicV3EndOfInterrupt(intid)`. `EndOfInterrupt()` is one of GiC AP's API, and it's called at the begining of `TimerInterruptHandler()`:

```
  //
  // DXE core uses this callback for the EFI timer tick. The DXE core uses locks
  // that raise to TPL_HIGH and then restore back to current level. Thus we need
  // to make sure TPL level is set to TPL_HIGH while we are handling the timer tick.
  //
  OriginalTPL = gBS->RaiseTPL (TPL_HIGH_LEVEL);

  // Signal end of interrupt early to help avoid losing subsequent ticks
  // from long duration handlers
  gInterrupt->EndOfInterrupt (gInterrupt, Source);
```

`ArmTimerDxe` debug log:

```
Loading driver at 0x001C18BD000 EntryPoint=0x001C18BE048 ArmTimerDxe.efi
InstallProtocolInterface: BC62157E-3E33-4FEC-9920-2D3B36D750DF 1C11F8798
ProtectUefiImageCommon - 0xC11F4040
  - 0x00000001C18BD000 - 0x0000000000009000
SetUefiImageMemoryAttributes - 0x00000001C18BD000 - 0x0000000000001000 (0x0000000000004008)
SetUefiImageMemoryAttributes - 0x00000001C18BE000 - 0x0000000000006000 (0x0000000000020008)
SetUefiImageMemoryAttributes - 0x00000001C18C4000 - 0x0000000000002000 (0x0000000000004008)
CoreStartImage(): Image->EntryPoint=0x1C18BE048
_ModuleEntryPoint() enters...
TimerInitialize() enters...
TimerDriverSetTimerPeriod(): TimerPeriod=0 (* 100 ns)
TimerDriverSetTimerPeriod(): ArmGenericTimerGetTimerFreq=25000000
TimerInitialize(): ArmGenericTimerGetTimerCtrlReg()=0x2
TimerInitialize(): TimerDriverGetTimerPeriod()=0
TimerInitialize(): about to register EL1 physical timer=30...
GicV3EnableInterruptSource() enters: source=30
ArmGicEnableInterrupt(GicD=0x20100000, GicR=0x20140000, Source=30) enters:
ArmGicEnableInterrupt(): GicCpuRedistributorBase=0x20140000, RegOffset=0, RegShift=30
ArmGicEnableInterrupt(): MmioWrite32() addr=0x20150100, val=0x40000000
ArmGicEnableInterrupt(): before write GICR_ISENABLER, ArmReadCntpCtl()=0x2
GicV3IrqInterruptHandler(): GicInterrupt=30
TimerInterruptHandler(): Source=30
GicV3IrqInterruptHandler(): GicInterrupt=30
TimerInterruptHandler(): Source=30
...
Synchronous Exception at 0x00000001C18EA108
PC 0x0001C18EA108 (0x0001C18E7000+0x00003108) [ 0] ArmGicDxe.dll
...
```

In `TimerInitialize()`, the logic seems the following:

- disable timer, by `ArmGenericTimerSetTimerCtrlReg()->ArmWriteCntpCtl()->msr cntp_ctl_el0, 2`. `cntp_ctl_el0` is "CouNTer-timer Physical timer ConTroL register", while `2` (`b10`) means `1`: masked/disabled, `0`: disabled. [ref](https://developer.arm.com/documentation/ddi0595/2020-12/AArch64-Registers/CNTP-CTL-EL0--Counter-timer-Physical-Timer-Control-register)
- set timer period = 0, which leads to a call to `ArmGenericTimerDisableTimer()`, which does the following:

    ```
    TimerCtrlReg = ArmReadCntpCtl();   // mrs x0, cntp_ctl_el0
    TimerCtrlReg &= ~ARM_ARCH_TIMER_ENABLE;
    ArmWriteCntpCtl(TimerCtrlReg);     // msr cntp_ctl_el0, x0
    ```

- register interrupt sources, via `gInterrupt->RegisterInterruptSource()`, for the 4 timers sources/INTIDs:
    - EL1 virtual timer: 27
    - Non-secure EL2 (Hyp) physical timer: 26
    - EL3 physical timer: 29
    - EL1 physical timer: 30

- Set timer period, via `TimerDriverSetTimerPeriod()`, which does the two things:
    - `ArmGenericTimerSetCompareVal()`: which maps to `ArmWriteCntpCval()`, and `msr cntp_cval_el0, x0`
    - `ArmGenericTimerEnableTimer()`: which is the opposite of `ArmGenericTimerDisableTimer()` shown above.
- enable timer, via `ArmGenericTimerSetTimerCtrlReg()`


From the log above, it seems that the interrupt 29 (or 30) happend before `TimerDriverSetTimerPeriod()`, which implies that `gInterrupt->RegisterInterruptSource()` effectively enables the timer interrput at the same time:

```
EFI_STATUS
EFIAPI
RegisterInterruptSource (
  IN EFI_HARDWARE_INTERRUPT_PROTOCOL    *This,
  IN HARDWARE_INTERRUPT_SOURCE          Source,
  IN HARDWARE_INTERRUPT_HANDLER         Handler
  )
{
  ...
  gRegisteredInterruptHandlers[Source] = Handler;
  if (NULL == Handler){
    return This->DisableInterruptSource (This, Source);
  } else {
    return This->EnableInterruptSource (This, Source);
  }
}
```

It seems that the following call directly enabled the timer interrupt (the next debug after the call never appears), i.e, no need to enable the timer by setting `cntp_ctl_el0`. And in the interrupt handler, `cntp_ctl_el0=3`, meaning `istatus=0`, `imask=1`, `ienable=1`. since `istatus=0`, `TimerInterruptHandler()` will neither call `CoreTimerTick()` nor reload the timer.

why?


```
This->EnableInterruptSource()
=GicV3EnableInterruptSource()
 `--ArmGicEnableInterrupt(GicD, GicR, Source)
    `-- MmioWrite32(ISENABLER_ADDRESS(GicCpuRedistributorBase, RegOffset), 1<<RegShift)
```

- When `CNTFRQ_EL0` is set? It seems it's set in EL1: `arm_bl1_platform_setup()->write_cntfrq_el0(plat_get_syscnt_freq2())`, and `plat_get_syscnt_freq2()` is implemented in `plat/MyCorp/common/MyCorp_common.c`.

How the timer interval is set? `TimerInitialize() -> TimerDriverSetTimerPeriod(FixedPcdGet32(PcdTimerPeriod))`, where `PcdTimerPeriod=100000`, meaning 1E5 in unit of 100ns, which is 1E7 ns (i.e., 10ms).



[Arm Gicv3 bare-metal example](https://github.com/NienfengYao/armv8-bare-metal)

Debug log from RPi4B:

```
oreStartImage() enters...
CoreStartImage(): Image->EntryPoint=0x3710E048
_ModuleEntryPoint() enters...
TimerInitialize() enters...
TimerDriverSetTimerPeriod(): TimerPeriod=0 (* 100 ns)
TimerDriverSetTimerPeriod(): ArmGenericTimerGetTimerFreq=54000000
TimerInitialize(): ArmGenericTimerGetTimerCtrlReg()=0x2
TimerInitialize(): TimerDriverGetTimerPeriod()=0
TimerInitialize(): set TimerDriverSetTimerPeriod() before RegisterInterruptSource ...
TimerDriverSetTimerPeriod(): TimerPeriod=100000 (* 100 ns)
TimerDriverSetTimerPeriod(): ArmGenericTimerGetTimerFreq=54000000
TimerDriverSetTimerPeriod(): mTimerTicks=540000
TimerInitialize(): now TimerDriverGetTimerPeriod()=100000
TimerInitialize(): PcdArmArchTimerVirtIntrNum=27 done!
TimerInitialize(): TimerHypIntrNum=26 done!
TimerInitialize(): about to register PcdArmArchTimerSecIntrNum=29...
TimerInitialize(): PcdArmArchTimerSecIntrNum=29 done!
TimerInitialize(): about to register EL1 physical timer=30...
TimerInitialize(): PcdArmArchTimerIntrNum=30 done!
TimerInitialize(): about to call  TimerDriverSetTimerPeriod()...
TimerDriverSetTimerPeriod(): TimerPeriod=100000 (* 100 ns)
TimerDriverSetTimerPeriod(): ArmGenericTimerGetTimerFreq=54000000
TimerDriverSetTimerPeriod(): mTimerTicks=540000
InstallProtocolInterface: 26BACCB3-6F42-11D4-BCE7-0080C73C8881 37115010
GenericProtocolNotify(): gEfiTimerArchProtocolGuid notify: to call gTimer->RegisterHandler (gTimer, CoreTimerTick)
TimerDriverRegisterHandler(): install notify function

TimerInterruptHandler(): Source=30. ArmGenericTimerGetTimerCtrlReg=0x5
TimerInterruptHandler(): - current=0xCC3E146, compare=0xCB586D6
TimerInterruptHandler(): mTimerNotifyFunction != 0
CoreTimerTick(): Duration=100000
TimerInterruptHandler(): + current=0xCCEBF88, compare=0xCD67C56

TimerInterruptHandler(): Source=30. ArmGenericTimerGetTimerCtrlReg=0x5
TimerInterruptHandler(): - current=0xCDB9DF4, compare=0xCD67C56
TimerInterruptHandler(): mTimerNotifyFunction != 0
CoreTimerTick(): Duration=400000
TimerInterruptHandler(): + current=0xCE67C1D, compare=0xCE6F716

TimerInterruptHandler(): Source=30. ArmGenericTimerGetTimerCtrlReg=0x5
TimerInterruptHandler(): - current=0xCF04794, compare=0xCE6F716
TimerInterruptHandler(): mTimerNotifyFunction != 0
CoreTimerTick(): Duration=200000
TimerInterruptHandler(): + current=0xCFB25BF, compare=0xCFFAF36
```

it shows that:

- `gInterrupt->RegisterInterruptSource()` does not enable the timer interrupt.
- only `INTID=30` triggered


2021.12.03: on FPGA:

```
GicV3DxeInitialize(): GICD_CTLR=12
GicV3DxeInitialize(): GICR_ICFGR1=0
GicV3DxeInitialize(): ICC_SRE_EL1=7
```

- `GICD_CTLR=0b1100`. Assuming that:
    - current PE security state: non-secure (as DXE expects)
    - the system support two two security state
    then the bit field is interpreted as:
    - bit[0]=0: since ARE_NS=0, this bit is an alias of `GICD_CTLR.EnableGrp1NS`
    - bit[1]=0: since ARE_NS=0, this bit is RES0
    - bit[3:2]: RES0
    - bit[4]=0: ARE_NS
- `GICR_ICFGR1=0`: PPI INTID 16~31 are all level-sensitive (the default)
- `ICC_SRE_EL1=0b111`:
    - bit[0]=1: IRQ/FIQ bypass disabled
    - bit[1]=1: IRQ/FIQ bypass disabled
    - bit[2]=1: system register access enabled

2021.12.03: MyChip PPI INTID assignment is different from SBSA recommended assginment:

- 23: Hyper Phy Timer
- 24: Hyper Virt Timer
- 25: Virt Timer
- 26: Phy Secure Timer
- 27: Phy Non-secure Timer

| Timer                | MyChip INTID | SBSA recommended INTID | note |
|:---------------------|:------------:|:----------------------:|:-----|
| EL1 phy              |   27         | 30                     | Dxe Timer |
| EL1 virt             |   25         | 27                     | |
| non-secure EL2 phy   |   23         | 26                     | |
| non-secure EL2 virt  |   24         | 28                     | |
| secure EL2 phy       |              | 20                     | |
| secure EL2 virt      |              | 19                     | |
| EL3 phy              |    26        | 29                     | |



The fix is to set the correct INTIDs in `MyChip.dsc` (commit id `00db867f`):

```
  gArmTokenSpaceGuid.PcdArmArchTimerHypIntrNum|24
  gArmTokenSpaceGuid.PcdArmArchTimerVirtIntrNum|25
  gArmTokenSpaceGuid.PcdArmArchTimerSecIntrNum|26
  gArmTokenSpaceGuid.PcdArmArchTimerIntrNum|27             # the Dxe Timer INTID
```

After that, the TimerDxe log shows the following sequence:

```
Loading driver 49EA041E-6752-42CA-B0B1-7344FE2546B7
InstallProtocolInterface: 5B1B31A1-9562-11D2-8E3F-00A0C969723B 1C11F4040
add-symbol-file /home/bruin/work/tianocore/Build/MyChip/NOOPT_GCC5/AARCH64/ArmPkg/Drivers/TimerDxe/TimerDxe/DEBUG/ArmTimerDxe.dll 0x1C18BE000
Loading driver at 0x001C18BD000 EntryPoint=0x001C18BE048 ArmTimerDxe.efi
InstallProtocolInterface: BC62157E-3E33-4FEC-9920-2D3B36D750DF 1C11F8798
ProtectUefiImageCommon - 0xC11F4040
  - 0x00000001C18BD000 - 0x0000000000009000
SetUefiImageMemoryAttributes - 0x00000001C18BD000 - 0x0000000000001000 (0x0000000000004008)
SetUefiImageMemoryAttributes - 0x00000001C18BE000 - 0x0000000000006000 (0x0000000000020008)
SetUefiImageMemoryAttributes - 0x00000001C18C4000 - 0x0000000000002000 (0x0000000000004008)
ProtectUefiImage() returned.
CoreStartImage() enters...
CoreStartImage(): Image->EntryPoint=0x1C18BE048
_ModuleEntryPoint() enters...
TimerInitialize() enters...
TimerDriverSetTimerPeriod(): TimerPeriod=0 (* 100 ns)
TimerDriverSetTimerPeriod(): ArmGenericTimerGetTimerFreq=25000000
TimerInitialize(): ArmGenericTimerGetTimerCtrlReg()=0x2
TimerInitialize(): TimerDriverGetTimerPeriod()=0
TimerInitialize(): set TimerDriverSetTimerPeriod() before RegisterInterruptSource ...
TimerDriverSetTimerPeriod(): TimerPeriod=10000000 (* 100 ns)
TimerDriverSetTimerPeriod(): ArmGenericTimerGetTimerFreq=25000000
TimerDriverSetTimerPeriod(): mTimerTicks=25000000
TimerInitialize(): now TimerDriverGetTimerPeriod()=10000000
TimerInitialize(): PcdArmArchTimerVirtIntrNum=25 done!
TimerInitialize(): TimerHypIntrNum=24 done!
TimerInitialize(): about to register PcdArmArchTimerSecIntrNum=26...
TimerInitialize(): PcdArmArchTimerSecIntrNum=26 done!
TimerInitialize(): about to register EL1 physical timer=27...
TimerInitialize(): PcdArmArchTimerIntrNum=27 done!
TimerInitialize(): about to call  TimerDriverSetTimerPeriod()...
TimerDriverSetTimerPeriod(): TimerPeriod=10000000 (* 100 ns)
TimerDriverSetTimerPeriod(): ArmGenericTimerGetTimerFreq=25000000
TimerDriverSetTimerPeriod(): mTimerTicks=25000000
InstallProtocolInterface: 26BACCB3-6F42-11D4-BCE7-0080C73C8881 1C18C4010
GenericProtocolNotify(): gEfiTimerArchProtocolGuid notify: to call gTimer->RegisterHandler (gTimer, CoreTimerTick)
TimerDriverRegisterHandler(): install notify function
After ProcessModuleEntryPointList

GicV3IrqInterruptHandler(): GicInterrupt=27, cntpct_el0=0x5E324C2A
TimerInterruptHandler(): Source=27. ArmGenericTimerGetTimerCtrlReg=0x5
TimerInterruptHandler(): - current=0x5E37882A, compare=0x5E3249C5
TimerInterruptHandler(): mTimerNotifyFunction != 0
CoreTimerTick(): Duration=10000000
TimerInterruptHandler(): + current=0x5E3D296E, compare=0x5FAFC205
...

Bds Arch Protocol not present!!

Variable Write Arch Protocol not present!!

Capsule Arch Protocol not present!!

Monotonic Counter Arch Protocol not present!!
Driver 42857F0A-13F2-4B21-8A23-53D3F714B840 was discovered but not loaded!!
Driver AD608272-D07F-4964-801E-7BD3B7888652 was discovered but not loaded!!

ASSERT_EFI_ERROR (Status = Not Found)
ASSERT [DxeCore] /home/bruin/work/tianocore/edk2/MdeModulePkg/Core/Dxe/DxeMain/DxeMain.c(538): !(((INTN)(RETURN_STATUS)(Status)) < 0)

```

### gEfiVariableWriteArchProtocolGuid bug

The problem was that `gEfiVariableWriteArchProtocolGuid` (`6441F818-6362-4E44-B570-7DBA31DD2453`) is never installed, thus two of its dependencies (Capsule and Monotonic Counter AP) will not be installed:

```
...
Bds Arch Protocol not present!!
Variable Write Arch Protocol not present!!
Capsule Arch Protocol not present!!
Monotonic Counter Arch Protocol not present!!
Driver 42857F0A-13F2-4B21-8A23-53D3F714B840 was discovered but not loaded!! <= Capsule
Driver AD608272-D07F-4964-801E-7BD3B7888652 was discovered but not loaded!! <= Monotonic

ASSERT_EFI_ERROR (Status = Not Found)
...
```

By comparing the booting flow on RPi4, it shows that `gEfiVariableWriteArchProtocolGuid` is installed inside the callback `FtwNotificationEvent()->VariableWriteServiceInitializeDxe()`. Actually the callback gets called twice:

- during loading/running `VariableRuntimeDxe.efi`: it checks that `FtwProtocol` is not installed yet, so just return.
- during loading/running `FaultTolerantWriteDxe.efi`, right after `FtwProtocol` is installed. then it check `GetFvbInfoByAddress()`, which uses a wrong `NvStorageVaraibleBase`. So the callback also returns, w/o calling `VariableWriteServiceInitializeDxe()`. That's the reason why `gEfiVariableWriteArchProtocolGuid` is never gets installed.

The fix is to give a correct value to `NvStorageVariableBase` (commit `05c1a52c536`). So the left error is what is expected:

```
...
Bds Arch Protocol not present!!
ASSERT_EFI_ERROR (Status = Not Found)
```

### Adding BDS module

Module/Lib need to customized:

- `edk2-platforms/Platform/RaspberryPi/Library/PlatformBootManagerLib/PlatformBootManagerLib.inf`
   - `PcdSdIsArasan`: [SD controller vendor](https://www.arasan.com/products/sd-emmc/sd-3-emmc-4-51-host/), default is 0.
- `edk2-non-osi/Platform/RaspberryPi/Drivers/LogoDxe/LogoDxe.inf`
- `edk2-platforms/Platform/RaspberryPi/Library/PlatformUiAppLib/PlatformUiAppLib.inf`

The error msg:

```
[Bds] Entry...
[Bds]BootManagerMenu FFS section can not be found, skip its boot option registration
[BdsDxe] Locate Variable Policy protocol - Success
Variable Driver Auto Update Lang, Lang:eng, PlatformLang:en-US Status: Success
!!! DEPRECATED INTERFACE !!! VariableLockRequestToLock() will go away soon!
!!! DEPRECATED INTERFACE !!! Please move to use Variable Policy!
!!! DEPRECATED INTERFACE !!! Variable: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C PlatformRecovery0000
ASSERT [BdsDxe] /home/bruin/work/tianocore/edk2-platforms/Platform/MyCorp/MyChip/Library/PlatformBootManagerLib/PlatformBm.c(578): 0 == 4
```

The assert is caused by `ASSERT (FixedPcdGet8 (PcdDefaultTerminalType) == 4);`. By checking RPi build report, `PcdDefaultTerminalType` is set to `4` in DSC. So we should do the same for MyChip.

After such a change, we got the following error:

```
[Bds] Entry...
[Bds]BootManagerMenu FFS section can not be found, skip its boot option registration
[BdsDxe] Locate Variable Policy protocol - Success
Variable Driver Auto Update Lang, Lang:eng, PlatformLang:en-US Status: Success
!!! DEPRECATED INTERFACE !!! VariableLockRequestToLock() will go away soon!
!!! DEPRECATED INTERFACE !!! Please move to use Variable Policy!
!!! DEPRECATED INTERFACE !!! Variable: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C PlatformRecovery0000
[Variable]END_OF_DXE is signaled
Initialize variable error flag (FF)
[Bds] No valid console instance is found for ConIn!   <= BmConsole.c:343
ASSERT [BdsDxe] /home/bruin/work/tianocore/edk2/MdePkg/Library/UefiLib/UefiLibPrint.c(63): Console != ((void *) 0)
```

Need to add more module/libs (Consoles, FDT, FAT, Shell), and customize some drivers (disable some functions for making it build success firstly):

- Platform/MyCorp/MyChip/Drivers/ConfigDxe/
- Platform/MyCorp/MyChip/Drivers/DisplayDxe/
- Platform/MyCorp/MyChip/Drivers/FdtDxe/

The next build issue is FV is too small. so we extend the max FD size to 2MiB, which also requires changes in ATF for FIP/BL33 max size definitions. At commit `e2e40b5c`, we have the following errors:

```
...
Driver 3ACEB0C0-3C72-11E4-9A56-74D435052646 was discovered but not loaded!!      <= TlsDxe
[Bds] Entry...
[Bds]BootManagerMenu FFS section can not be found, skip its boot option registration
[BdsDxe] Locate Variable Policy protocol - Success
Variable Driver Auto Update Lang, Lang:eng, PlatformLang:en-US Status: Success
!!! DEPRECATED INTERFACE !!! VariableLockRequestToLock() will go away soon!
!!! DEPRECATED INTERFACE !!! Please move to use Variable Policy!
!!! DEPRECATED INTERFACE !!! Variable: 8BE4DF61-93CA-11D2-AA0D-00E098032B8C PlatformRecovery0000
[Variable]END_OF_DXE is signaled
Initialize variable error flag (FF)
Terminal - Mode 0, Column = 80, Row = 25
Terminal - Mode 1, Column = 80, Row = 50
Terminal - Mode 2, Column = 100, Row = 31
InstallProtocolInterface: 387477C1-69C7-11D2-8E39-00A0C969723B 1BCD4C040
InstallProtocolInterface: DD9E7534-7762-4698-8C14-F58517A625AA 1BCD4C128
InstallProtocolInterface: 387477C2-69C7-11D2-8E39-00A0C969723B 1BCD4C058
InstallProtocolInterface: 09576E91-6D3F-11D2-8E39-00A0C969723B 1BCD4BB18
InstallProtocolInterface: D3B36F2C-D551-11D4-9A46-0090273FC14D 0
InstallProtocolInterface: D3B36F2D-D551-11D4-9A46-0090273FC14D 0
InstallProtocolInterface: D3B36F2B-D551-11D4-9A46-0090273FC14D 0
ESC (setup), F1 (shell), ENTER (boot)Evaluate DXE DEPEX for FFS(3ACEB0C0-3C72-11E4-9A56-74D435052646)
  PUSH GUID(3152BCA5-EADE-433D-862E-C01CDC291F44) = FALSE
  PUSH GUID(665E3FF6-46CC-11D4-9A38-0090273FC14D) = TRUE
  PUSH GUID(26BACCB1-6F42-11D4-BCE7-0080C73C8881) = TRUE
  PUSH GUID(26BACCB2-6F42-11D4-BCE7-0080C73C8881) = TRUE
  PUSH GUID(1DA97072-BDDC-4B30-99F1-72A0B56FFF2A) = TRUE
  PUSH GUID(27CFAC87-46CC-11D4-9A38-0090273FC14D) = TRUE
  PUSH GUID(27CFAC88-46CC-11D4-9A38-0090273FC14D) = TRUE
  PUSH GUID(B7DFB4E1-052F-449F-87BE-9818FC91B733) = TRUE
  PUSH GUID(A46423E3-4617-49F1-B9FF-D1BFA9115839) = TRUE
  PUSH GUID(26BACCB3-6F42-11D4-BCE7-0080C73C8881) = TRUE
  PUSH GUID(6441F818-6362-4E44-B570-7DBA31DD2453) = TRUE
  PUSH GUID(1E5668E2-8481-11D4-BCF1-0080C73C8881) = TRUE
  PUSH GUID(665E3FF5-46CC-11D4-9A38-0090273FC14D) = TRUE
  AND
  AND
  AND
  AND
  AND
  AND
  AND
  AND
  AND
  AND
  AND
  AND
  END
  RESULT = FALSE
Evaluate DXE DEPEX for FFS(3ACEB0C0-3C72-11E4-9A56-74D435052646)
  PUSH GUID(3152BCA5-EADE-433D-862E-C01CDC291F44) = FALSE   <= gEfiRngProtocolGuid
  PUSH GUID(665E3FF6-46CC-11D4-9A38-0090273FC14D) = TRUE
  PUSH GUID(26BACCB1-6F42-11D4-BCE7-0080C73C8881) = TRUE
  PUSH GUID(26BACCB2-6F42-11D4-BCE7-0080C73C8881) = TRUE
  PUSH GUID(1DA97072-BDDC-4B30-99F1-72A0B56FFF2A) = TRUE
  PUSH GUID(27CFAC87-46CC-11D4-9A38-0090273FC14D) = TRUE
  PUSH GUID(27CFAC88-46CC-11D4-9A38-0090273FC14D) = TRUE
  PUSH GUID(B7DFB4E1-052F-449F-87BE-9818FC91B733) = TRUE
  PUSH GUID(A46423E3-4617-49F1-B9FF-D1BFA9115839) = TRUE
  PUSH GUID(26BACCB3-6F42-11D4-BCE7-0080C73C8881) = TRUE
  PUSH GUID(6441F818-6362-4E44-B570-7DBA31DD2453) = TRUE
  PUSH GUID(1E5668E2-8481-11D4-BCF1-0080C73C8881) = TRUE
  PUSH GUID(665E3FF5-46CC-11D4-9A38-0090273FC14D) = TRUE
  AND
  AND
  AND
  AND
  AND
  AND
  AND
  AND
  AND
  AND
  AND
  AND
  END
  RESULT = FALSE
[Bds]RegisterKeyNotify: 000B/0000 80000000/00 Success
[Bds]RegisterKeyNotify: 0000/000D 80000000/00 Success
[Bds]BootManagerMenu FFS section can not be found, skip its boot option registration

ASSERT_EFI_ERROR (Status = Not Found)
ASSERT [BdsDxe] /home/bruin/work/tianocore/edk2-platforms/Platform/MyCorp/MyChip/Library/PlatformBootManagerLib/PlatformBm.c(515): !(((INTN)(RETURN_STATUS)(Status)) < 0)
```

### Rng driver

The log above shows that `TlsDxe` cannot be loaded because RNG protocol is not installed. It seems that RaspberryPi has a dedicated RNG HW. For MyChip, after searching the soruce tree, it seems that we can leverage `edk2/SecurityPkg/RandomNumberGenerator/RngDxe/RngDxe.inf`.

But, as tested on FPGA, it seems that there is a loop dependency: `RngDxe.efi` (`B981A835-...`) depends on `gEfiRngProtocolGuid`, which is to be installed by the same driver! According to bhe build log, the dependency is caused by one of the drivers lib, which is `RngLib|MdePkg/Library/DxeRngLib/DxeRngLib.inf`, which depends on `gEfiRngProtocolGuid`.

```
Evaluate DXE DEPEX for FFS(B981A835-6EE8-4F4C-AE0B-210AA0BFBF01)  <= RngDxe.efi, which insalls gEfiPngProdocolGuid
  PUSH GUID(13A3F0F6-264A-3EF0-F2E0-DEC512342F34) = TRUE          <= gEfiPcdProtocolGuid
  PUSH GUID(3152BCA5-EADE-433D-862E-C01CDC291F44) = FALSE         <= gEfiPngProtocolGuid
  AND
  END
  RESULT = FALSE
```

Possible solutions:

- Change the `RngLib` instance, to, e.g., `edk2/MdePkg/Library/BaseRngLib/BaseRngLib.inf`. But it seems that this library requires CPU support `RNDR` instruction, which is FALSE on MyChip FPGA (this implies that `FEAT_RNG=False` for MyChip)! thus it abort at `edk2/MdePkg/Library/BaseRngLib/AArch64/Rndr.c`.
- Override the DEPEX explicitly somehow?

[stackoverflow question](https://stackoverflow.com/questions/70273497/edk2-possible-loop-dependency-in-rngdxe-driver)

### How BDS launches boot-mgr and shell

- In DXE phase, When loading/starting `Bds.efi`, the `gEfiBdsArchProtocolGuid` (`665e3ff6-46cc-11d4-9a38-0090273fc14d`) will be installed in `BdsInitialize()`.  The `gEfiBdsArchProtocolGuid` contains only one function `Entry()`.
- DxeCore maintains a global pointer `gBds`, which is assigned to the correct value when the protocol is installed.
- DxeCore calls `gBds->Entry()` at the end of `DxeMain()` after it dispatched all loadable modules and all required Arch Protocols are available.
- `gBds->Entry()` maps to `BdsEntry.c:BdsEntry()`.


```
[Bds]BootManagerMenu FFS section can not be found, skip its boot option registration
```

The above log is caused by setting of `gEfiMdeModulePkgTokenSpaceGuid.PcdBootManagerMenuFile`. This should be corresponding to the FFS GUID of `UiApp` (reported in build report as `462CAA21-7614-4503-836E-8AB6F4662331`, the 1st 3 fileds are numbers), so the PCD value in little-endian should be `{ 0x21, 0xaa, 0x2c, 0x46, 0x14, 0x76, 0x03, 0x45, 0x83, 0x6e, 0x8a, 0xb6, 0xf4, 0x66, 0x23, 0x31 }`.

After that, we can enter into the Shell! (commit `0984ca2d`).

The Shell response is very slow: change `gEmbeddedTokenSpaceGuid.PcdTimerPeriod` from 1s to 0.1s

```
...
map: No mapping found.
Press ESC in 1 seconds to skip startup.nsh or any other key to continue.
Shell>
Shell> ver
UEFI Interactive Shell v2.2
EDK II
UEFI v2.70 (EDK2, 0x00010000)
Shell> date
12/09/2021
Shell> dh
Handle dump
01: LoadedImage(DxeCore)
02: Decompress
03: FirmwareVolume2 DevicePath(..0xB,0x102000000,0x1021DFFFF)) FirmwareVolumeBlock
04: FirmwareVolume2 DevicePath(..A38E-4B13-CF52-22A90E6FE662)) FirmwareVolumeBlock
05: FC1BCDB0-7D31-49AA-936A-A4600D9DD083
06: ImageDevicePath(..87AB-47F9-A3FE-D50B76D89541)) LoadedImage(PcdDxe)
07: GetPcdInfo GetPcdInfoProtocol Pcd Pcd
08: ImageDevicePath(..43B7-4784-95B1-F4226CB40CEE)) LoadedImage(RuntimeDxe)
09: RuntimeArch
0A: ImageDevicePath(..7FD6-4665-8646-88E33EF71DFC)) LoadedImage(SecurityStubDxe)
0B: SecurityArch Security2Arch
0C: DeferredImageLoad
0D: ImageDevicePath(..B23F-4B92-BC8E-FB01CE5907B7)) LoadedImage(VarBlockServiceDxe)
0E: DevicePath(..0xB,0x1021E0000,0x1021FFFFF)) FirmwareVolumeBlock
0F: ImageDevicePath(..7068-4FF5-B462-9822B4AD8D60)) LoadedImage(VariableRuntimeDxe)
10: VariableWriteArch 81D1675C-86F6-48DF-BD95-9A6E4F0925C3 VariableArch AF23B340-97B4-4685-8D4F-A3F28169B21D CD3D0A05-9E24-437C-A891-1EE053DB7638
11: ImageDevicePath(..E8EF-46D0-953C-9B8E96527D13)) LoadedImage(Reset)
12: ResetArch
13: ImageDevicePath(..C77D-410D-8100-1495911A989D)) LoadedImage(MetronomeDxe)
14: MetronomeArch
15: ImageDevicePath(..BFBD-4882-9ECE-C80BB1C4783B)) LoadedImage(HiiDatabase)
16: HiiImageEx HIIImage ConfigKeywordHandler HIIConfigRouting HIIDatabase HIIString HIIFont
17: ImageDevicePath(..5C29-453F-825C-837A46A81E15)) LoadedImage(SerialDxe)
18: DevicePath(..EB627241)/Uart(115200,8,N,1)) SerialIO
19: ImageDevicePath(..DEC4-4D21-ADF1-593ABCC15882)) LoadedImage(ArmGicDxe)
1A: 32898322-2DA1-474A-BAAA-F3F7CF569470 2890B3EA-053D-1643-AD0C-D64808DA3FF1
1B: ImageDevicePath(..109E-437E-9FE4-1AA09C7074D9)) LoadedImage(FdtDxe)
1C: DebugSupport 96F46153-97A7-4793-ACC1-FA19BF78EA97 EBCInterpreter ImageDevicePath(..73D0-11D4-B06B-00AA00BD6DE7)) LoadedImage(EbcDxe)
1D: AAEACCFD-F27B-4C17-B610-75CA1F2DFB52
1E: ImageDevicePath(..AD6B-4F3A-B60B-F59899003443)) LoadedImage(DevicePathDxe)
1F: DevicePathFromText DevicePathToText DevicePathUtilities
20: ImageDevicePath(..229D-4F4D-AA37-9895E6C9EABA)) LoadedImage(DpcDxe)
21: 480F8AE9-0C46-4AA9-BC89-DB9FBA619806
22: ImageDevicePath(..E72A-11E4-91F9-28D2447C4829)) LoadedImage(HttpUtilitiesDxe)
23: HttpUtilities
24: ImageDevicePath(..D72A-451F-9BDB-BAFB52A68415)) LoadedImage(ArmCpuDxe)
25: CpuArch
26: ImageDevicePath(..4F72-49E8-986F-2CD899DFFE5D)) LoadedImage(FaultTolerantWriteDxe)
27: 3EBD9E82-2C78-4DE6-9786-8D4BFCB7C881
28: ImageDevicePath(..4135-4A55-AE4E-4971BBF0885D)) LoadedImage(RealTimeClock)
29: RealTimeClockArch
2A: ImageDevicePath(..B23F-4B92-BC8E-FB01CE5907B7)) LoadedImage(ConfigDxe)
2B: ImageDevicePath(..6752-42CA-B0B1-7344FE2546B7)) LoadedImage(ArmTimerDxe)
2C: TimerArch
2D: ImageDevicePath(..284E-4B47-A984-FD66B482DAC0)) LoadedImage(BootManagerPolicyDxe)
2E: BootManagerPolicy
2F: ImageDevicePath(..B1D3-4EF8-957C-8048606FF671)) LoadedImage(SetupBrowser)
30: HIIFormBrowser2
31: 1F73B18D-4630-43C1-A1DE-6F80855D7DA4 A770C357-B693-4E6D-A6CF-D21C728E550B
32: ImageDevicePath(..EC75-4855-A54D-809C75241F6C)) LoadedImage(BdsDxe)
33: BdsArch
34: HiiPackageList ImageDevicePath(..37E7-48FC-97F7-9B1047749C69)) LoadedImage(LogoDxe)
35: 53CD299F-2BC1-40C0-8C07-23F64FDB30E0
36: ImageDevicePath(..13F2-4B21-8A23-53D3F714B840)) LoadedImage(CapsuleRuntimeDxe)
37: CapsuleArch
38: ImageDevicePath(..D07F-4964-801E-7BD3B7888652)) LoadedImage(MonotonicCounterRuntimeDxe)
39: MonotonicCounterArch
3A: ImageDevicePath(..0EFC-46FB-9137-4F2DA8F419F3)) LoadedImage(ConsolePrefDxe)
3B: DevicePath(..E96C-484D-B2DD-7C2EDFC7D56F))
3C: ImageDevicePath(..71AE-4C36-B2A3-DCEB0EB2B7D8)) LoadedImage(WatchdogTimer)
3D: WatchdogTimerArch
3E: ImageDevicePath(..058E-4B55-A54B-F02F83A24707)) LoadedImage(DisplayEngine)
3F: HiiPopup 9BBE29E9-FDA1-41EC-AD52-452213742D2E
40: ImageDevicePath(..0DD1-4787-84F1-F48D537DCACF)) LoadedImage(DriverHealthManagerDxe)
41: HIIConfigAccess DevicePath(..0DD1-4787-84F1-F48D537DCACF))
42: 7CA1024F-EB17-11E5-9DBA-28D2447C4829 ImageDevicePath(..EB17-11E5-9DBA-28D2447C4829)) LoadedImage(TlsAuthConfigDxe)
43: HIIConfigAccess DevicePath(..EB17-11E5-9DBA-28D2447C4829))
44: HIIConfigAccess DevicePath(..9A04-4C6D-A748-793DAA0F65DF))
45: ComponentName2 ComponentName DriverBinding ImageDevicePath(..4FDF-4E55-A45B-E123F84D456A)) LoadedImage(ConPlatformDxe)
46: ComponentName2 ComponentName DriverBinding
47: ComponentName2 ComponentName DriverBinding ImageDevicePath(..CF6D-477C-A5A8-B4844E3DE281)) LoadedImage(ConSplitterDxe)
48: ComponentName2 ComponentName DriverBinding
49: ComponentName2 ComponentName DriverBinding
4A: ComponentName2 ComponentName DriverBinding
4B: ComponentName2 ComponentName DriverBinding
4C: AbsolutePointer SimplePointer SimpleTextInEx SimpleTextIn
4D: SimpleTextOut
4E: SimpleTextOut
4F: ComponentName2 ComponentName DriverBinding ImageDevicePath(..A40F-4875-977F-5B93FF237FC6)) LoadedImage(TerminalDxe)
50: ImageDevicePath(..FAD2-4030-841B-CFC9644D2C5B)) LoadedImage(DisplayDxe)
51: ComponentName2 ComponentName DriverBinding ImageDevicePath(..AD98-40E9-9093-ACA2B5A253C4)) LoadedImage(DiskIoDxe)
52: ComponentName2 ComponentName DriverBinding ImageDevicePath(..FEFF-4AAE-BD7B-38A070A3B609)) LoadedImage(PartitionDxe)
53: ComponentName2 ComponentName DriverBinding ImageDevicePath(..B6B7-44C3-AF35-6BC705CD2B1F)) LoadedImage(Fat)
54: ImageDevicePath(..50FB-4FE8-8E4E-AB74D2C1A600)) LoadedImage(EnglishDxe)
55: UnicodeCollation2 UnicodeCollation
56: ComponentName2 ComponentName DriverBinding ImageDevicePath(..A127-4EF8-957C-8048606FF670)) LoadedImage(SnpDxe)
57: ComponentName2 ComponentName DriverBinding ImageDevicePath(..FE2C-4B56-A8F4-08519BC439DF)) LoadedImage(VlanConfigDxe)
58: ComponentName2 ComponentName DriverBinding ImageDevicePath(..E6A9-4B8B-82AD-6815A1AEAF4A)) LoadedImage(MnpDxe)
59: ComponentName2 ComponentName DriverBinding ImageDevicePath(..E8E9-4E73-B1E1-BDF6A9D50113)) LoadedImage(ArpDxe)
5A: ComponentName2 ComponentName DriverBinding ImageDevicePath(..0BBC-47FB-96A5-EE7A5AE6A2AD)) LoadedImage(Dhcp4Dxe)
5B: ComponentName2 ComponentName DriverBinding ImageDevicePath(..3B71-4324-B39A-745CBB015FFF)) LoadedImage(Ip4Dxe)
5C: ComponentName2 ComponentName DriverBinding ImageDevicePath(..906D-4A65-A7CA-BD40E5D6AF2B)) LoadedImage(Udp4Dxe)
5D: ComponentName2 ComponentName DriverBinding ImageDevicePath(..2FA8-4ED3-BC1F-F9962A03454B)) LoadedImage(Mtftp4Dxe)
5E: ComponentName2 ComponentName DriverBinding ImageDevicePath(..34BE-4775-A651-7EA41B69D89E)) LoadedImage(Dhcp6Dxe)
5F: ComponentName2 ComponentName DriverBinding ImageDevicePath(..D830-4EB2-8742-2D4CC9B54F2C)) LoadedImage(Ip6Dxe)
60: ComponentName2 ComponentName DriverBinding ImageDevicePath(..F098-4367-92BA-E911083C7B0E)) LoadedImage(Udp6Dxe)
61: ComponentName2 ComponentName DriverBinding ImageDevicePath(..98D8-49DD-A8D3-3219D0FFE41E)) LoadedImage(Mtftp6Dxe)
62: ComponentName2 ComponentName DriverBinding ImageDevicePath(..2F55-4A56-903C-01265EB7622B)) LoadedImage(TcpDxe)
63: ComponentName2 ComponentName DriverBinding
64: ComponentName2 ComponentName DriverBinding ImageDevicePath(..26DE-48D2-8807-1F9107AC5E3A)) LoadedImage(UefiPxeBcDxe)
65: ComponentName2 ComponentName DriverBinding
66: ComponentName2 ComponentName DriverBinding ImageDevicePath(..DFFC-11E3-B956-0022681E6906)) LoadedImage(DnsDxe)
67: ComponentName2 ComponentName DriverBinding
68: ComponentName2 ComponentName DriverBinding ImageDevicePath(..E15A-11E3-8BF1-E4115B28BC50)) LoadedImage(HttpDxe)
69: ComponentName2 ComponentName DriverBinding
6A: ComponentName2 ComponentName DriverBinding ImageDevicePath(..D9C8-11E4-AF3D-8CDCD426C973)) LoadedImage(HttpBootDxe)
6B: ComponentName2 ComponentName DriverBinding
6C: ConsoleIn StdErr ConsoleOut DevicePath(..5BB1-458C-A48F-E25FDD51EF94)) SimpleTextOut SimpleTextInEx SimpleTextIn
6D: Shell ShellParameters SimpleTextOut ImageDevicePath(..9E3E-4F1C-AD65-E05268D0B4D1)) LoadedImage(Shell)
Shell>
Shell> bcfg driver dump
No options found.
Shell> bcfg boot dump -v
Option: 00. Variable: Boot0000
  Desc    - UiApp
  DevPath - Fv(56CEF77F-A38E-4B13-CF52-22A90E6FE662)/FvFile(462CAA21-7614-4503-8
36E-8AB6F4662331)
  Optional- N
Option: 01. Variable: Boot0001
  Desc    - UEFI Shell
  DevPath - Fv(56CEF77F-A38E-4B13-CF52-22A90E6FE662)/FvFile(7C04A583-9E3E-4F1C-A
D65-E05268D0B4D1)
  Optional- N
```

### Push edk2 related repositories to gerrit

2021.12.10:

- upload `edk2`/`edk2-platforms`/`edk2-non-osi`/`edk2-libc` to NOMACHINE (`/home/shareToAll/`), after:
    - `git clean -fxd`
    - `git pull`
- ask Admin(HouHai) to:
    - create 4 empty repositories on git/gerrit
    - temp enable direct push priviledges
- do the following on NOMACHINE for each repo. (take `edk2-libc` as example):
    - get the target/new clone url of the repo from gerrit web page: `$ export REPO="ssh://bruin.xiong@gerrit.idc.MyCorp.com:29418/MyCorpSW/edk2-libc.git"`.
    - `$ cd edk2-libc`: this is the folder cloned from github.
    - `$ git remote rename origin old-origin`: this is to keep the old origin in the config. check `.git/config` and `.git/refs/remotes` for effects. Another way is to completely remove the old origin, by `$ git remote rm origin`.
    - `$ git remote add origin $REPO`
    - `$ git push -u origin --all`
    - `$ git push -u origin --tags`
        - `-u`: `--set-upstream`, add tracking branches under `.git/refs/remotes/origin/`
        - `--all`: all branches
        - `--tags`: all tags
    - test the repo by `$ git clone $REPO`: in case encounter error msg `warning: remote HEAD refers to nonexistent ref, unable to checkout`, ask Admin(HouHai) to check access rights assigned to the current user (e.g., read right).
- As `edk2` repo which contains 7 submodules (from 6 repos), create 6 more empty repos on gerrit, and repeat the procedure above. Now we should have six repositories:

    ```
    ssh://gerrit.idc.MyCorp.com:29418/MyCorpSW/edk2-submodules/openssl
    ssh://gerrit.idc.MyCorp.com:29418/MyCorpSW/edk2-submodules/berkeley-softfloat-3
    ssh://gerrit.idc.MyCorp.com:29418/MyCorpSW/edk2-submodules/oniguruma
    ssh://gerrit.idc.MyCorp.com:29418/MyCorpSW/edk2-submodules/brotli
    ssh://gerrit.idc.MyCorp.com:29418/MyCorpSW/edk2-submodules/jansson
    ssh://gerrit.idc.MyCorp.com:29418/MyCorpSW/edk2-submodules/edk2-cmocka
    ```

    Note that there are issues to push the last one `edk2-cmocka.git` as it's empty. However, this submodule can be ignored safely.

  Then:

    ```
    git clone ssh://bruin.xiong@gerrit.idc.MyCorp.com:29418/MyCorpSW/edk2
    cd edk2
    vi .gitmodules   # replace submodule's url with new ones as shown above
    git submodule init
    git submodule update
    git diff .
    diff --git a/.gitmodules b/.gitmodules
    index b845c9ee3f..6090c88b61 100644
    --- a/.gitmodules
    +++ b/.gitmodules
    @@ -1,22 +1,22 @@
     [submodule "CryptoPkg/Library/OpensslLib/openssl"]
            path = CryptoPkg/Library/OpensslLib/openssl
    -       url = https://github.com/openssl/openssl
    +       url = ssh://gerrit.idc.MyCorp.com:29418/MyCorpSW/edk2-submodules/openssl
     [submodule "SoftFloat"]
            path = ArmPkg/Library/ArmSoftFloatLib/berkeley-softfloat-3
    -       url = https://github.com/ucb-bar/berkele
    ...
    git add .gitmodules
    git commit -m "update submodules' urls"
    git push origin master
    ```

- inform Admin(HouHai) to disable direct push priviledges

### `dmpstore` 分析

refs:

- http://kurtqiao.github.io/uefi/2015/01/13/uefi-boot-manager.html
- https://oofhours.com/2019/09/02/geeking-out-with-uefi/

```
Shell> help dmpstore
Manages all UEFI variables.

DMPSTORE [-b] [-d] [-all | ([variable] [-guid guid])] [-sfo]
DMPSTORE [-all | ([variable] [-guid guid])] [-s file]
DMPSTORE [-all | ([variable] [-guid guid])] [-l file]

  -b       - Displays one screen at a time.
  -guid    - Specifies the GUID of the variables to be displayed in
             standard text format. If not specified and -all is not
             specified, the EFI_GLOBAL_VARIABLE GUID is assumed.
  -sfo     - Displays information as described in Standard-Format Output.
  -all     - Dumps all variables, including those
             with a different GUID than EFI_GLOBAL_VARIABLE.
  -d       - Delete variables.
  -s       - Saves variables to a file.
  -l       - Loads and sets variables from a file.
  variable - Specifies a variable name. This can be a literal name or
             a pattern as specified in the MetaiMatch() function of the
             EFI_UNICODE_COLLATION2_PROCOOL.

NOTES:
  1. This command manages the UEFI variables. The variables
     displayed or deleted depend on the command line options, as specified in
     the following table:
     Variable GUID  -all  Description
     ---      ---   ---   All variables with the GUID EFI_GLOBAL_VARIABLE will
                          be operated on.
     ---      ---    X    All variables (regardless of GUID or name) will be
                          operated on.
     ---       X    ---   All variables with the specified GUID will be
                          operated on.
      X       ---   ---   The variable with the GUID EFI_GLOBAL_VARIABLE and
                          the name Variable will be operated on.
      X        X    ---   The variable with the specified GUID and name
                          Variable will be operated on.
  2. The variable value is printed as a hexadecimal dump.
  3. Option -d is used to delete variables. Option -s and -l are used to save
     and load variables to and from a file. The variable name can be specified
     when using these flags so that the operation only takes effect on
     that variable.

EXAMPLES:
  * To dump all variables with the GUID EFI_GLOBAL_VARIABLE:
    Shell> dmpstore

  * To dump all variables (regardless of GUID or name):
    Shell> dmpstore -all

  * To dump the 'path' variable with the GUID '158DEF5A-F656-419C-B027-
    7A3192C079D2':
    Shell> dmpstore path -guid 158DEF5A-F656-419C-B027-7A3192C079D2

  * To save all variables (regardless of GUID or name) to a file 'VarDump.txt':
    fs0:\> dmpstore -all -s VarDump.txt-4FDC-A22A-E5F46812F4CA 1BCD2FD18
 nstallProtocolInterface: 6302D008-7F9B-4F30-87AC-60C9FEF5DA4E 1BA928710
  * To delete the 'BootOrder' variable with the GUID EFI_GLOBAL_VARIABLE:
    Shell> dmpstore -d BootOrder
Shell> dmpstore -all
Variable NV+BS '4C19049F-4137-4DD3-9C10-8B97A83FFDFA:MemoryTypeInformation' Data
Size = 0x50
  00000000: 09 00 00 00 00 00 00 00-0A 00 00 00 00 00 00 00  *................*
  00000010: 00 00 00 00 00 00 00 00-06 00 00 00 34 03 00 00  *............4...*
  00000020: 05 00 00 00 D0 02 00 00-03 00 00 00 19 05 00 00  *................*
  00000030: 04 00 00 00 E0 2E 00 00-01 00 00 00 14 00 00 00  *................*
  00000040: 02 00 00 00 00 00 00 00-0F 00 00 00 00 00 00 00  *................*
Variable NV+RT+BS 'EFIGlobalVariable:Key0001' DataSize = 0x0E
  00000000: 00 00 00 40 91 3F AA 11-00 00 17 00 00 00        *...@.?........*
Variable NV+RT+BS 'EFIGlobalVariable:Key0000' DataSize = 0x0E
  00000000: 00 00 00 40 C2 13 1C D6-01 00 0B 00 00 00        *...@..........*
Variable NV+RT+BS 'EFIGlobalVariable:Boot0001' DataSize = 0x48
  00000000: 00 00 00 00 2C 00 55 00-45 00 46 00 49 00 20 00  *....,.U.E.F.I. .*
  00000010: 53 00 68 00 65 00 6C 00-6C 00 00 00 04 07 14 00  *S.h.e.l.l.......*
  00000020: 7F F7 CE 56 8E A3 13 4B-CF 52 22 A9 0E 6F E6 62  *...V...K.R"..o.b*
  00000030: 04 06 14 00 83 A5 04 7C-3E 9E 1C 4F AD 65 E0 52  *.......|>..O.e.R*
  00000040: 68 D0 B4 D1 7F FF 04 00-                         *h.......*
Variable NV+RT+BS 'EFIGlobalVariable:BootOrder' DataSize = 0x04
  00000000: 00 00 01 00                                      *....*
Variable NV+RT+BS '5B6F7107-BB3C-4660-92CD-542690280BBD:BootDiscoveryPolicy' Dat
aSize = 0x04
  00000000: 02 00 00 00                                      *....*
Variable NV+RT+BS '04B37FE8-F6AE-480B-BDD5-37D98C5E89AA:VarErrorFlag' DataSize =
 0x01
  00000000: FF                                               *.*
Variable NV+RT+BS 'EFIGlobalVariable:ErrOut' DataSize = 0x3F
  00000000: 01 04 14 00 4B 7D 98 D3-1A 97 5F 43 8C AF 49 67  *....K}...._C..Ig*
  00000010: EB 62 72 41 03 0E 13 00-00 00 00 00 00 C2 01 00  *.brA............*
  00000020: 00 00 00 00 08 01 01 03-0A 14 00 80 6D 91 7D B1  *............m.}.*
  00000030: 5B 8C 45 A4 8F E2 5F DD-51 EF 94 7F FF 04 00     *[.E..._.Q......*
Variable NV+RT+BS 'EFIGlobalVariable:ConOut' DataSize = 0x3F
  00000000: 01 04 14 00 4B 7D 98 D3-1A 97 5F 43 8C AF 49 67  *....K}...._C..Ig*
  00000010: EB 62 72 41 03 0E 13 00-00 00 00 00 00 C2 01 00  *.brA............*
  00000020: 00 00 00 00 08 01 01 03-0A 14 00 80 6D 91 7D B1  *............m.}.*
  00000030: 5B 8C 45 A4 8F E2 5F DD-51 EF 94 7F FF 04 00     *[.E..._.Q......*
Variable NV+RT+BS 'EFIGlobalVariable:ConIn' DataSize = 0x4E
  00000000: 03 0F 0B 00 FF FF FF FF-03 01 01 7F 01 04 00 01  *................*
  00000010: 04 14 00 4B 7D 98 D3 1A-97 5F 43 8C AF 49 67 EB  *...K}...._C..Ig.*
  00000020: 62 72 41 03 0E 13 00 00-00 00 00 00 C2 01 00 00  *brA.............*
  00000030: 00 00 00 08 01 01 03 0A-14 00 80 6D 91 7D B1 5B  *...........m.}.[*
  00000040: 8C 45 A4 8F E2 5F DD 51-EF 94 7F FF 04 00        *.E..._.Q......*
Variable NV+RT+BS 'EFIGlobalVariable:Lang' DataSize = 0x04
  00000000: 65 6E 67 00                                      *eng.*
Variable NV+RT+BS 'EFIGlobalVariable:PlatformLang' DataSize = 0x06
  00000000: 65 6E 2D 55 53 00                                *en-US.*
Variable NV+RT+BS 'EFIGlobalVariable:Timeout' DataSize = 0x02
  00000000: 05 00                                            *..*
Variable NV+RT+BS 'EFIGlobalVariable:Boot0000' DataSize = 0x3E
  00000000: 09 01 00 00 2C 00 55 00-69 00 41 00 70 00 70 00  *....,.U.i.A.p.p.*
  00000010: 00 00 04 07 14 00 7F F7-CE 56 8E A3 13 4B CF 52  *.........V...K.R*
  00000020: 22 A9 0E 6F E6 62 04 06-14 00 21 AA 2C 46 14 76  *"..o.b....!.,F.v*
  00000030: 03 45 83 6E 8A B6 F4 66-23 31 7F FF 04 00        *.E.n...f#1....*
Variable NV+RT+BS 'B336F62D-4135-4A55-AE4E-4971BBF0885D:RtcDaylight' DataSize =
0x01
  00000000: 00                                               *.*
Variable NV+RT+BS 'B336F62D-4135-4A55-AE4E-4971BBF0885D:RtcTimeZone' DataSize =
0x02
  00000000: FF 07                                            *..*
Variable NV+RT+BS 'B336F62D-4135-4A55-AE4E-4971BBF0885D:RtcEpochSeconds' DataSiz
e = 0x08
  00000000: 55 CC B6 61 00 00 00 00-                         *U..a....*
Variable NV+BS '2D2358B4-E96C-484D-B2DD-7C2EDFC7D56F:ConsolePref' DataSize = 0x0
4
  00000000: 00 00 00 00                                      *....*
Variable NV+RT+BS 'EB704011-1402-11D3-8E77-00A0C969723B:MTC' DataSize = 0x04
  00000000: 01 00 00 00                                      *....*
Variable BS '158DEF5A-F656-419C-B027-7A3192C079D2:lasterror' DataSize = 0x08
  00000000: 30 00 78 00 31 00 35 00-                         *0.x.1.5.*
Variable BS '158DEF5A-F656-419C-B027-7A3192C079D2:debuglasterror' DataSize = 0x0
8
  00000000: 30 00 78 00 31 00 35 00-                         *0.x.1.5.*
Variable BS '158DEF5A-F656-419C-B027-7A3192C079D2:uefiversion' DataSize = 0x08
  00000000: 32 00 2E 00 37 00 30 00-                         *2...7.0.*
Variable BS '158DEF5A-F656-419C-B027-7A3192C079D2:uefishellversion' DataSize = 0
x06
  00000000: 32 00 2E 00 32 00                                *2...2.*
Variable BS '158DEF5A-F656-419C-B027-7A3192C079D2:uefishellsupport' DataSize = 0
x02
  00000000: 33 00                                            *3.*
Variable BS '158DEF5A-F656-419C-B027-7A3192C079D2:profiles' DataSize = 0x44
  00000000: 3B 00 44 00 72 00 69 00-76 00 65 00 72 00 31 00  *;.D.r.i.v.e.r.1.*
  00000010: 3B 00 44 00 65 00 62 00-75 00 67 00 31 00 3B 00  *;.D.e.b.u.g.1.;.*
  00000020: 6E 00 65 00 74 00 77 00-6F 00 72 00 6B 00 31 00  *n.e.t.w.o.r.k.1.*
  00000030: 3B 00 61 00 63 00 70 00-69 00 76 00 69 00 65 00  *;.a.c.p.i.v.i.e.*
  00000040: 77 00 3B 00                                      *w.;.*
Variable BS '0053D9D6-2659-4599-A26B-EF4536E631A9:ren' DataSize = 0x06
  00000000: 6D 00 76 00 00 00                                *m.v...*
Variable BS '0053D9D6-2659-4599-A26B-EF4536E631A9:move' DataSize = 0x06
  00000000: 6D 00 76 00 00 00                                *m.v...*
Variable BS '0053D9D6-2659-4599-A26B-EF4536E631A9:mount' DataSize = 0x08
  00000000: 6D 00 61 00 70 00 00 00-                         *m.a.p...*
Variable BS '0053D9D6-2659-4599-A26B-EF4536E631A9:mem' DataSize = 0x0A
  00000000: 64 00 6D 00 65 00 6D 00-00 00                    *d.m.e.m...*
Variable BS '0053D9D6-2659-4599-A26B-EF4536E631A9:md' DataSize = 0x0C
  00000000: 6D 00 6B 00 64 00 69 00-72 00 00 00              *m.k.d.i.r...*
Variable BS '0053D9D6-2659-4599-A26B-EF4536E631A9:dir' DataSize = 0x06
  00000000: 6C 00 73 00 00 00                                *l.s...*
Variable BS '0053D9D6-2659-4599-A26B-EF4536E631A9:del' DataSize = 0x06
  00000000: 72 00 6D 00 00 00                                *r.m...*
Variable BS '0053D9D6-2659-4599-A26B-EF4536E631A9:copy' DataSize = 0x06
  00000000: 63 00 70 00 00 00                                *c.p...*
Variable BS '0053D9D6-2659-4599-A26B-EF4536E631A9:cd\' DataSize = 0x0A
  00000000: 63 00 64 00 20 00 5C 00-00 00                    *c.d. .\...*
Variable BS '0053D9D6-2659-4599-A26B-EF4536E631A9:cd..' DataSize = 0x0C
  00000000: 63 00 64 00 20 00 2E 00-2E 00 00 00              *c.d. .......*
Variable BS '0053D9D6-2659-4599-A26B-EF4536E631A9:cat' DataSize = 0x0A
  00000000: 74 00 79 00 70 00 65 00-00 00                    *t.y.p.e...*
Variable BS '158DEF5A-F656-419C-B027-7A3192C079D2:nonesting' DataSize = 0x0A
  00000000: 46 00 61 00 6C 00 73 00-65 00                    *F.a.l.s.e.*
Variable RT+BS 'EFIGlobalVariable:BootCurrent' DataSize = 0x02
  00000000: 01 00                                            *..*
Variable RT+BS 'EFIGlobalVariable:ErrOutDev' DataSize = 0x237
  00000000: 01 04 14 00 4B 7D 98 D3-1A 97 5F 43 8C AF 49 67  *....K}...._C..Ig*
  00000010: EB 62 72 41 03 0E 13 00-00 00 00 00 00 C2 01 00  *.brA............*
  00000020: 00 00 00 00 08 01 01 03-0A 14 00 53 47 C1 E0 BE  *...........SG...*
  00000030: F9 D2 11 9A 0C 00 90 27-3F C1 4D 7F 01 04 00 01  *.......'?.M.....*
  00000040: 04 14 00 4B 7D 98 D3 1A-97 5F 43 8C AF 49 67 EB  *...K}...._C..Ig.*
  00000050: 62 72 41 03 0E 13 00 00-00 00 00 00 C2 01 00 00  *brA.............*
  00000060: 00 00 00 08 01 01 03 0A-14 00 65 60 A6 DF 19 B4  *..........e`....*
  00000070: D3 11 9A 2D 00 90 27 3F-C1 4D 7F 01 04 00 01 04  *...-..'?.M......*
  00000080: 14 00 4B 7D 98 D3 1A 97-5F 43 8C AF 49 67 EB 62  *..K}...._C..Ig.b*
  00000090: 72 41 03 0E 13 00 00 00-00 00 00 C2 01 00 00 00  *rA..............*
  000000A0: 00 00 08 01 01 03 0A 14-00 0B C7 AE 7B E0 57 76  *............{.Wv*
  000000B0: 4C 8E 87 2F 9E 28 08 83-43 7F 01 04 00 01 04 14  *L../.(..C.......*
  000000C0: 00 4B 7D 98 D3 1A 97 5F-43 8C AF 49 67 EB 62 72  *.K}...._C..Ig.br*
  000000D0: 41 03 0E 13 00 00 00 00-00 00 C2 01 00 00 00 00  *A...............*
  000000E0: 00 08 01 01 03 0A 14 00-D6 A0 15 AD EC 8B CF 4A  *...............J*
  000000F0: A0 73 D0 1D E7 7E 2D 88-7F 01 04 00 01 04 14 00  *.s...~-.........*
  00000100: 4B 7D 98 D3 1A 97 5F 43-8C AF 49 67 EB 62 72 41  *K}...._C..Ig.brA*
  00000110: 03 0E 13 00 00 00 00 00-00 C2 01 00 00 00 00 00  *................*
  00000120: 08 01 01 03 0A 14 00 80-6D 91 7D B1 5B 8C 45 A4  *........m.}.[.E.*
  00000130: 8F E2 5F DD 51 EF 94 7F-01 04 00 01 04 14 00 4B  *.._.Q..........K*
  00000140: 7D 98 D3 1A 97 5F 43 8C-AF 49 67 EB 62 72 41 03  *}...._C..Ig.brA.*
  00000150: 0E 13 00 00 00 00 00 00-C2 01 00 00 00 00 00 08  *................*
  00000160: 01 01 03 0A 14 00 7F 4A-36 E4 25 F8 0E 43 9D 3A  *.......J6.%..C.:*
  00000170: 9C 9B E6 81 7C A5 7F 01-04 00 01 04 14 00 4B 7D  *....|.........K}*
  00000180: 98 D3 1A 97 5F 43 8C AF-49 67 EB 62 72 41 03 0E  *...._C..Ig.brA..*
  00000190: 13 00 00 00 00 00 00 C2-01 00 00 00 00 00 08 01  *................*
  000001A0: 01 03 0A 14 00 6B A5 FC-FB 36 BB 78 4B AA AB BE  *.....k...6.xK...*
  000001B0: 1B 97 EC 7C CB 7F 01 04-00 01 04 14 00 4B 7D 98  *...|.........K}.*
  000001C0: D3 1A 97 5F 43 8C AF 49-67 EB 62 72 41 03 0E 13  *..._C..Ig.brA...*
  000001D0: 00 00 00 00 00 00 C2 01-00 00 00 00 00 08 01 01  *................*
  000001E0: 03 0A 14 00 DD DD 46 8E-49 3D 9D 4A B8 75 3C 08  *......F.I=.J.u<.*
  000001F0: 6F 6A A2 BD 7F 01 04 00-01 04 14 00 4B 7D 98 D3  *oj..........K}..*
  00000200: 1A 97 5F 43 8C AF 49 67-EB 62 72 41 03 0E 13 00  *.._C..Ig.brA....*
  00000210: 00 00 00 00 00 C2 01 00-00 00 00 00 08 01 01 03  *................*
  00000220: 0A 14 00 E0 D6 7D FC 3C-81 4D 43 B4 DA 3B D6 49  *.....}.<.MC..;.I*
  00000230: E9 E1 5A 7F FF 04 00                             *..Z....*
Variable RT+BS 'EFIGlobalVariable:ConOutDev' DataSize = 0x237
  00000000: 01 04 14 00 4B 7D 98 D3-1A 97 5F 43 8C AF 49 67  *....K}...._C..Ig*
  00000010: EB 62 72 41 03 0E 13 00-00 00 00 00 00 C2 01 00  *.brA............*
  00000020: 00 00 00 00 08 01 01 03-0A 14 00 53 47 C1 E0 BE  *...........SG...*
  00000030: F9 D2 11 9A 0C 00 90 27-3F C1 4D 7F 01 04 00 01  *.......'?.M.....*
  00000040: 04 14 00 4B 7D 98 D3 1A-97 5F 43 8C AF 49 67 EB  *...K}...._C..Ig.*
  00000050: 62 72 41 03 0E 13 00 00-00 00 00 00 C2 01 00 00  *brA.............*
  00000060: 00 00 00 08 01 01 03 0A-14 00 65 60 A6 DF 19 B4  *..........e`....*
  00000070: D3 11 9A 2D 00 90 27 3F-C1 4D 7F 01 04 00 01 04  *...-..'?.M......*
  00000080: 14 00 4B 7D 98 D3 1A 97-5F 43 8C AF 49 67 EB 62  *..K}...._C..Ig.b*
  00000090: 72 41 03 0E 13 00 00 00-00 00 00 C2 01 00 00 00  *rA..............*
  000000A0: 00 00 08 01 01 03 0A 14-00 0B C7 AE 7B E0 57 76  *............{.Wv*
  000000B0: 4C 8E 87 2F 9E 28 08 83-43 7F 01 04 00 01 04 14  *L../.(..C.......*
  000000C0: 00 4B 7D 98 D3 1A 97 5F-43 8C AF 49 67 EB 62 72  *.K}...._C..Ig.br*
  000000D0: 41 03 0E 13 00 00 00 00-00 00 C2 01 00 00 00 00  *A...............*
  000000E0: 00 08 01 01 03 0A 14 00-D6 A0 15 AD EC 8B CF 4A  *...............J*
  000000F0: A0 73 D0 1D E7 7E 2D 88-7F 01 04 00 01 04 14 00  *.s...~-.........*
  00000100: 4B 7D 98 D3 1A 97 5F 43-8C AF 49 67 EB 62 72 41  *K}...._C..Ig.brA*
  00000110: 03 0E 13 00 00 00 00 00-00 C2 01 00 00 00 00 00  *................*
  00000120: 08 01 01 03 0A 14 00 80-6D 91 7D B1 5B 8C 45 A4  *........m.}.[.E.*
  00000130: 8F E2 5F DD 51 EF 94 7F-01 04 00 01 04 14 00 4B  *.._.Q..........K*
  00000140: 7D 98 D3 1A 97 5F 43 8C-AF 49 67 EB 62 72 41 03  *}...._C..Ig.brA.*
  00000150: 0E 13 00 00 00 00 00 00-C2 01 00 00 00 00 00 08  *................*
  00000160: 01 01 03 0A 14 00 7F 4A-36 E4 25 F8 0E 43 9D 3A  *.......J6.%..C.:*
  00000170: 9C 9B E6 81 7C A5 7F 01-04 00 01 04 14 00 4B 7D  *....|.........K}*
  00000180: 98 D3 1A 97 5F 43 8C AF-49 67 EB 62 72 41 03 0E  *...._C..Ig.brA..*
  00000190: 13 00 00 00 00 00 00 C2-01 00 00 00 00 00 08 01  *................*
  000001A0: 01 03 0A 14 00 6B A5 FC-FB 36 BB 78 4B AA AB BE  *.....k...6.xK...*
  000001B0: 1B 97 EC 7C CB 7F 01 04-00 01 04 14 00 4B 7D 98  *...|.........K}.*
  000001C0: D3 1A 97 5F 43 8C AF 49-67 EB 62 72 41 03 0E 13  *..._C..Ig.brA...*
  000001D0: 00 00 00 00 00 00 C2 01-00 00 00 00 00 08 01 01  *................*
  000001E0: 03 0A 14 00 DD DD 46 8E-49 3D 9D 4A B8 75 3C 08  *......F.I=.J.u<.*
  000001F0: 6F 6A A2 BD 7F 01 04 00-01 04 14 00 4B 7D 98 D3  *oj..........K}..*
  00000200: 1A 97 5F 43 8C AF 49 67-EB 62 72 41 03 0E 13 00  *.._C..Ig.brA....*
  00000210: 00 00 00 00 00 C2 01 00-00 00 00 00 08 01 01 03  *................*
  00000220: 0A 14 00 E0 D6 7D FC 3C-81 4D 43 B4 DA 3B D6 49  *.....}.<.MC..;.I*
  00000230: E9 E1 5A 7F FF 04 00                             *..Z....*
Variable RT+BS 'EFIGlobalVariable:ConInDev' DataSize = 0x237
  00000000: 01 04 14 00 4B 7D 98 D3-1A 97 5F 43 8C AF 49 67  *....K}...._C..Ig*
  00000010: EB 62 72 41 03 0E 13 00-00 00 00 00 00 C2 01 00  *.brA............*
  00000020: 00 00 00 00 08 01 01 03-0A 14 00 53 47 C1 E0 BE  *...........SG...*
  00000030: F9 D2 11 9A 0C 00 90 27-3F C1 4D 7F 01 04 00 01  *.......'?.M.....*
  00000040: 04 14 00 4B 7D 98 D3 1A-97 5F 43 8C AF 49 67 EB  *...K}...._C..Ig.*
  00000050: 62 72 41 03 0E 13 00 00-00 00 00 00 C2 01 00 00  *brA.............*
  00000060: 00 00 00 08 01 01 03 0A-14 00 65 60 A6 DF 19 B4  *..........e`....*
  00000070: D3 11 9A 2D 00 90 27 3F-C1 4D 7F 01 04 00 01 04  *...-..'?.M......*
  00000080: 14 00 4B 7D 98 D3 1A 97-5F 43 8C AF 49 67 EB 62  *..K}...._C..Ig.b*
  00000090: 72 41 03 0E 13 00 00 00-00 00 00 C2 01 00 00 00  *rA..............*
  000000A0: 00 00 08 01 01 03 0A 14-00 0B C7 AE 7B E0 57 76  *............{.Wv*
  000000B0: 4C 8E 87 2F 9E 28 08 83-43 7F 01 04 00 01 04 14  *L../.(..C.......*
  000000C0: 00 4B 7D 98 D3 1A 97 5F-43 8C AF 49 67 EB 62 72  *.K}...._C..Ig.br*
  000000D0: 41 03 0E 13 00 00 00 00-00 00 C2 01 00 00 00 00  *A...............*
  000000E0: 00 08 01 01 03 0A 14 00-D6 A0 15 AD EC 8B CF 4A  *...............J*
  000000F0: A0 73 D0 1D E7 7E 2D 88-7F 01 04 00 01 04 14 00  *.s...~-.........*
  00000100: 4B 7D 98 D3 1A 97 5F 43-8C AF 49 67 EB 62 72 41  *K}...._C..Ig.brA*
  00000110: 03 0E 13 00 00 00 00 00-00 C2 01 00 00 00 00 00  *................*
  00000120: 08 01 01 03 0A 14 00 80-6D 91 7D B1 5B 8C 45 A4  *........m.}.[.E.*
  00000130: 8F E2 5F DD 51 EF 94 7F-01 04 00 01 04 14 00 4B  *.._.Q..........K*
  00000140: 7D 98 D3 1A 97 5F 43 8C-AF 49 67 EB 62 72 41 03  *}...._C..Ig.brA.*
  00000150: 0E 13 00 00 00 00 00 00-C2 01 00 00 00 00 00 08  *................*
  00000160: 01 01 03 0A 14 00 7F 4A-36 E4 25 F8 0E 43 9D 3A  *.......J6.%..C.:*
  00000170: 9C 9B E6 81 7C A5 7F 01-04 00 01 04 14 00 4B 7D  *....|.........K}*
  00000180: 98 D3 1A 97 5F 43 8C AF-49 67 EB 62 72 41 03 0E  *...._C..Ig.brA..*
  00000190: 13 00 00 00 00 00 00 C2-01 00 00 00 00 00 08 01  *................*
  000001A0: 01 03 0A 14 00 6B A5 FC-FB 36 BB 78 4B AA AB BE  *.....k...6.xK...*
  000001B0: 1B 97 EC 7C CB 7F 01 04-00 01 04 14 00 4B 7D 98  *...|.........K}.*
  000001C0: D3 1A 97 5F 43 8C AF 49-67 EB 62 72 41 03 0E 13  *..._C..Ig.brA...*
  000001D0: 00 00 00 00 00 00 C2 01-00 00 00 00 00 08 01 01  *................*
  000001E0: 03 0A 14 00 DD DD 46 8E-49 3D 9D 4A B8 75 3C 08  *......F.I=.J.u<.*
  000001F0: 6F 6A A2 BD 7F 01 04 00-01 04 14 00 4B 7D 98 D3  *oj..........K}..*
  00000200: 1A 97 5F 43 8C AF 49 67-EB 62 72 41 03 0E 13 00  *.._C..Ig.brA....*
  00000210: 00 00 00 00 00 C2 01 00-00 00 00 00 08 01 01 03  *................*
  00000220: 0A 14 00 E0 D6 7D FC 3C-81 4D 43 B4 DA 3B D6 49  *.....}.<.MC..;.I*
  00000230: E9 E1 5A 7F FF 04 00                             *..Z....*
Variable RT+BS 'EFIGlobalVariable:PlatformRecovery0000' DataSize = 0x6E
  00000000: 01 00 00 00 36 00 44 00-65 00 66 00 61 00 75 00  *....6.D.e.f.a.u.*
  00000010: 6C 00 74 00 20 00 50 00-6C 00 61 00 74 00 66 00  *l.t. .P.l.a.t.f.*
  00000020: 6F 00 72 00 6D 00 52 00-65 00 63 00 6F 00 76 00  *o.r.m.R.e.c.o.v.*
  00000030: 65 00 72 00 79 00 00 00-04 04 32 00 5C 00 45 00  *e.r.y.....2.\.E.*
  00000040: 46 00 49 00 5C 00 42 00-4F 00 4F 00 54 00 5C 00  *F.I.\.B.O.O.T.\.*
  00000050: 42 00 4F 00 4F 00 54 00-41 00 41 00 36 00 34 00  *B.O.O.T.A.A.6.4.*
  00000060: 2E 00 45 00 46 00 49 00-00 00 7F FF 04 00        *..E.F.I.......*
Variable RT+BS 'EFIGlobalVariable:PlatformLangCodes' DataSize = 0x06
  00000000: 65 6E 2D 55 53 00                                *en-US.*
Variable RT+BS 'EFIGlobalVariable:LangCodes' DataSize = 0x0D
  00000000: 65 6E 67 66 72 61 65 6E-67 66 72 61 00           *engfraengfra.*
Variable RT+BS 'EFIGlobalVariable:BootOptionSupport' DataSize = 0x04
  00000000: 13 03 00 00                                      *....*
Variable RT+BS 'EFIGlobalVariable:OsIndicationsSupported' DataSize = 0x08
  00000000: 41 00 00 00 00 00 00 00-                         *A.......*
Shell>
```

How to interprete the content of `ConIn/ConOut/ErrOut` variables above?

> The `ConIn`, `ConOut`, and `ErrOut` variables each contains an `EFI_DEVICE_PATH` descriptor that defines the default device to use on boot.
>
> --- Beyond BIOS, 3rd Ed, p190

Take `ErrOut` Device Path as example:

```
Variable NV+RT+BS 'EFIGlobalVariable:ErrOut' DataSize = 0x3F
  00000000: 01 04 14 00 4B 7D 98 D3-1A 97 5F 43 8C AF 49 67  *....K}...._C..Ig*
  00000010: EB 62 72 41 03 0E 13 00-00 00 00 00 00 C2 01 00  *.brA............*
  00000020: 00 00 00 00 08 01 01 03-0A 14 00 80 6D 91 7D B1  *............m.}.*
  00000030: 5B 8C 45 A4 8F E2 5F DD-51 EF 94 7F FF 04 00     *[.E..._.Q......*
```

It contains 4 Device Path Nodes:

1. HwVendor:

```
  00000000: 01 04 14 00 4B 7D 98 D3-1A 97 5F 43 8C AF 49 67
  00000010: EB 62 72 41

typedef struct {
  EFI_DEVICE_PATH_PROTOCOL Header;
  EFI_GUID                 Guid;      <= EDKII_SERIAL_PORT_LIB_VENDOR_GUID
} VENDOR_DEVICE_PATH;

typedef struct {
  UINT8 Type;                         <= 01: HARDWARE_DEVICE_PATH
  UINT8 SubType;                      <= 04: HW_VENDOR_DP
  UINT8 Length[2];                    <= 14 00: sizeof(VENDOR_DEVICE_PATH)
} EFI_DEVICE_PATH_PROTOCOL;

#define EDKII_SERIAL_PORT_LIB_VENDOR_GUID { \
          0xD3987D4B, 0x971A, 0x435F, \
          { 0x8C, 0xAF, 0x49, 0x67, 0xEB, 0x62, 0x72, 0x41 } \
          }
```

2. Uart:

```
  00000010:             03 0E 13 00-00 00 00 00 00 C2 01 00
  00000020: 00 00 00 00 08 01 01

typedef struct {
  EFI_DEVICE_PATH_PROTOCOL Header;      <= 03: Type (MESSAGING_DEVICE_PATH)
                                        <= 0E: SubType (MSG_UART_DP)
                                        <= 13 00: sizeof(UART_DEVICE_PATH)
  UINT32                   Reserved;    <= 00 00 00 00
  UINT64                   BaudRate;    <= 00 C2 01 00 00 00 00 00: 115200=0x01c200
  UINT8                    DataBits;    <= 08
  UINT8                    Parity;      <= 01
  UINT8                    StopBits;    <= 01
} UART_DEVICE_PATH;
```

3. TtyTerm:

```
  00000020:                      03-0A 14 00 80 6D 91 7D B1
  00000030: 5B 8C 45 A4 8F E2 5F DD-51 EF 94

typedef struct {
  EFI_DEVICE_PATH_PROTOCOL Header;    <= 03: Type (MESSAGING_DEVICE_PATH)
                                      <= 0A: SubType (MSG_VENDOR_DP)
                                      <= 14 00: sizeof(VENDOR_DEVICE_PATH)
  EFI_GUID                 Guid;      <= gEfiTtyTermGuid (EFI_TTY_TERM_GUID)
} VENDOR_DEVICE_PATH;
```

4. End of Hardware Device Path

```
  00000030:                                  7F FF 04 00

typedef struct {
  UINT8 Type;                         <= 7f: end of hardware device path
  UINT8 SubType;                      <= ff: end entire device path
  UINT8 Length[2];                    <= 04 00: sizeof(EFI_DEVICE_PATH_PROTOCOL)
} EFI_DEVICE_PATH_PROTOCOL;
```

The setting of the Device Path can be found inside function `PlatformBootManagerBeforeConsole()` in
`MyChip/Library/PlatformBootManagerLib/PlatformBm.c`, particularly the `mSerialConsole` variable.

```
STATIC PLATFORM_SERIAL_CONSOLE mSerialConsole = {
  // VENDOR_DEVICE_PATH SerialDxe
  {
    { HARDWARE_DEVICE_PATH, HW_VENDOR_DP, DP_NODE_LEN (VENDOR_DEVICE_PATH) },
    SERIAL_DXE_FILE_GUID
  },
  // UART_DEVICE_PATH Uart
  {
    { MESSAGING_DEVICE_PATH, MSG_UART_DP, DP_NODE_LEN (UART_DEVICE_PATH) },
    0,                                      // Reserved
    FixedPcdGet64 (PcdUartDefaultBaudRate), // BaudRate
    FixedPcdGet8 (PcdUartDefaultDataBits),  // DataBits
    FixedPcdGet8 (PcdUartDefaultParity),    // Parity
    FixedPcdGet8 (PcdUartDefaultStopBits)   // StopBits
  },
  // VENDOR_DEFINED_DEVICE_PATH TermType
  {
    {
      MESSAGING_DEVICE_PATH, MSG_VENDOR_DP,
      DP_NODE_LEN (VENDOR_DEFINED_DEVICE_PATH)
    }
    // Guid to be filled in dynamically
  },
  // EFI_DEVICE_PATH_PROTOCOL End
  {
    END_DEVICE_PATH_TYPE, END_ENTIRE_DEVICE_PATH_SUBTYPE,
    DP_NODE_LEN (EFI_DEVICE_PATH_PROTOCOL)
  }
};
```

`ConIn` is a bit different, that it contains two device pathes, the 1st one is USB keyboard (`mUsbKeyboard`):

```
Variable NV+RT+BS 'EFIGlobalVariable:ConIn' DataSize = 0x4E
  00000000: 03 0F 0B 00 FF FF FF FF-03 01 01 7F 01 04 00

typedef struct {
  UINT8 Type;                         <= 7f: end of hardware device path
  UINT8 SubType;                      <= 01: End This Instance of a Device Path and start a new one
  UINT8 Length[2];                    <= 04 00: sizeof(EFI_DEVICE_PATH_PROTOCOL)
} EFI_DEVICE_PATH_PROTOCOL;
```

### SerialDXE revisited

The `SerialLib` is `SerialPortLib|Platform/MyCorp/MyChip/Library/DwApbSerialPortLib/DwApbSerialPortLib.inf`.

For PEI phase, the `SerialLib` is supplied to `PeiUniCore.inf`:

```
  ArmPlatformPkg/PrePi/PeiUniCore.inf {
    <LibraryClasses>
      SerialPortLib|Platform/MyCorp/MyChip/Library/DwApbSerialPortLib/DwApbSerialPortLib.inf
  }
```

Note that `PeiUniCore.inf` indicates that no protocol is produced by this module.

For DXE phase, the same `SerialLib` is supplied to `SerialDxe.inf`:

```
  MdeModulePkg/Universal/SerialDxe/SerialDxe.inf {
    <LibraryClasses>
      SerialPortLib|Platform/MyCorp/MyChip/Library/DwApbSerialPortLib/DwApbSerialPortLib.inf
  }
```

And `SerialDxe.inf` indicates that it produces two protocols:

```
[Protocols]
  gEfiSerialIoProtocolGuid      ## PRODUCES
  gEfiDevicePathProtocolGuid    ## PRODUCES
```

The code in `edk2/MdeModulePkg/Universal/SerialDxe/SerialIo.c:SerialDxeInitialize()` shows exactly that:

```
  //
  // Make a new handle with Serial IO protocol and its device path on it.
  //
  Status = gBS->InstallMultipleProtocolInterfaces (
                  &mSerialHandle, // it's NULL as input
                  &gEfiSerialIoProtocolGuid,   &mSerialIoTemplate,
                  &gEfiDevicePathProtocolGuid, &mSerialDevicePath,
                  NULL
                  );
```

The IO protocol variable `mSerialIoTemplate` is of type `EFI_SERIAL_IO_PROTOCOL`:

```
struct _EFI_SERIAL_IO_PROTOCOL {
  UINT32                      Revision;
  EFI_SERIAL_RESET            Reset;
  EFI_SERIAL_SET_ATTRIBUTES   SetAttributes;
  EFI_SERIAL_SET_CONTROL_BITS SetControl;
  EFI_SERIAL_GET_CONTROL_BITS GetControl;
  EFI_SERIAL_WRITE            Write;
  EFI_SERIAL_READ             Read;
  EFI_SERIAL_IO_MODE          *Mode;
  CONST EFI_GUID              *DeviceTypeGuid;
};
typedef struct _EFI_SERIAL_IO_PROTOCOL EFI_SERIAL_IO_PROTOCOL;
```

And the member functions maps to those provided in `SerialPortLib`.

The Device Path protocol `mSerialDevicePath` contains GUID and uart parameters, and the GUID is set to `EDKII_SERIAL_PORT_LIB_VENDOR_GUID`.

What can be learnt here? Probabaly: For adding DXE drivers for a new platform, the first thing is to identify what *UEFI standard protocols* are required for that driver. From the protocols definitions we know which functions to be implemented. To find out the required protocols for a driver, do the following:

- find a sample DXE driver
- find out which protocols the sample driver installed

### FdtDxe

FIXME:

### MMC driver

Refs:

- https://en.wikipedia.org/wiki/SD_card
- http://www.wowotech.net/basic_tech/mmc_sd_sdio_intro.html
- https://www.sdcard.org/downloads/pls/
- https://blog.csdn.net/gaojy19881225/article/details/105601561
- https://blog.csdn.net/kivy_xian/article/details/53333831

MyChip on FPGA is using standard `sdhci` in `arch/arm64/boot/dts/MyCorp/MyCorp_MyChip.dtsi`:

```
sd: sdhci@20000000 {
    compatible = "MyCorp,snps-sdhci";
    reg = <0x0 0x20000000 0x0 0x1000>;
    interrupts = <GIC_SPI 10 IRQ_TYPE_LEVEL_HIGH>;
    bus-width = <4>;
    no-1-8-v;
    no-sdio;
    no-mmc;
};
```

As shown above, the base address is `0x2000_0000`, which was assigned to DMA in MyChip. This means that this address is "borrowed" from DMA to MMC/SD, which is only valid for an updated bitfile on FPGA. On MyChip ASIC chip, this address is not availabe for MMC/SD.

The card used for testing is a 16G SanDisk SD card (9 pin, 24x32mm). The pin assignment of 4-bit transfer mode can be found [here](https://en.wikipedia.org/wiki/SD_card#Transfer_modes).

The 1st step is to find a reference platform which uses the DesignWare IP for SD controller (`dwc_mshc`/`dwc_mshc_lite`).

Possible Sd/Mmc driver-candidates in edk2 ` find . -type d|grep "Emmc\|Mmc\|Sd"`:

```
./edk2/MdeModulePkg/Bus/Sd/EmmcDxe
./edk2/MdeModulePkg/Bus/Sd/EmmcBlockIoPei
./edk2/MdeModulePkg/Bus/Sd/SdBlockIoPei
./edk2/MdeModulePkg/Bus/Sd/SdDxe
./edk2/MdeModulePkg/Bus/Pci/SdMmcPciHcPei
./edk2/MdeModulePkg/Bus/Pci/SdMmcPciHcDxe
./edk2/EmbeddedPkg/Universal/MmcDxe
./edk2-platforms/Platform/RaspberryPi/Drivers/ArasanMmcHostDxe: Arasan SDHCI
./edk2-platforms/Platform/RaspberryPi/Drivers/MmcDxe: Broadcom sdhost
./edk2-platforms/Silicon/Synopsys/DesignWare/Drivers/DwEmmcDxe: used by `Platform/Hisilicon/HiKey/HiKey.dsc`:
./edk2-platforms/Silicon/Marvell/Drivers/SdMmc
./edk2-platforms/Silicon/Marvell/Drivers/SdMmc/XenonDxe
./edk2-platforms/Silicon/TexasInstruments/Omap35xxPkg/MmcHostDxe
```
> If there is no PCI bus, you could implement a fake one. Just like what we did at `edk2-platforms/Silicon/TexasInstruments/Omap35xxPkg/PciEmulation`. Through this way, you can reuse SdMmcPciHc driver.
>
> The EDKII SD/MMC stack (`SdMmcPciHcDxe` plus `SdDxe` and `EmmcDxe`) is used to manage
all SD & MMC host controllers & cards. Each SD & MMC host controller would be
installed a EFI_SD_MMC_PASS_THRU_PROTOCOL instance. We distinguish the card
types by identification process defined in SD & EMMC spec. after that, we will
install different device paths through which upper layer could distinguish them.
>
> For SD host controller, the device path is Pci(x, x)\Sd(x). for EMMC host
controller, the device path is Pci(x, x)\EMMC(x)\Ctrl(x). why we appended a
Ctrl(x) device node to EMMC device path is because EMMC device has many
partitions (User Data Area, BOOT1&2, GP1&2&3&4, RPMB). We use Ctrl(x) to
distinguish the partitions. But SD is different story, it has no partitions, so
we just produce Pci(x, x)\Sd(x) to distinguish different SD HCs if they exist.
>
> --- https://www.mail-archive.com/edk2-devel@lists.01.org/msg14664.html

## RPi4B?

In `dsc` file:

```
  Platform/RaspberryPi/Drivers/ArasanMmcHostDxe/ArasanMmcHostDxe.inf
  Platform/RaspberryPi/Drivers/MmcDxe/MmcDxe.inf
```

- `edk2-platforms/Silicon/Broadcom/Bcm283x/Include/IndustryStandard/Bcm2836Sdio.h/Bcm236Sdio.h`: MMC/SD/SDIO1 register definitions.

> The Pi 4 added a new SD controller that supports DDR50. The Arasan controller that used to be on the SD card is now used for the WiFi. The sdhost controller that was on WiFi is now spare.
>
> --- [What has been changed on Pi 4's SD/MMC interface?](https://forums.raspberrypi.com/viewtopic.php?t=248244)

- DDR50: double data rate with clock at 50MHz

> The BCM283x family includes two SD card controllers; one is an Arasan SDHCI compliant controller (sdhc(4) driver) and another internal SD HOST controller (the new sdhost(4) driver).
>
> Up until now, we have been using the SDHCI controller to drive the SD card slot. The SD HOST controller cannot do SDIO, so using it for the SD card slot will allow us to free up the SDHCI controller for use with the Wi-Fi chip on the Pi 3 and Zero W boards.
>
> --- https://mail-index.netbsd.org/port-arm/2017/07/30/msg004328.html

## HiKey?

- [What is 96boards?](https://www.96boards.org/about/)
- [hikey 96boards](https://www.96boards.org/documentation/consumer/hikey/)
    - [Hikey(HiKey620)](https://www.96boards.org/documentation/consumer/hikey/hikey620/): Hisilicon Kirin 6220
        - [Hikey620 hardware docs](https://github.com/96boards/documentation/blob/master/consumer/hikey/hikey620/hardware-docs/)
    - [HiKey960](https://www.96boards.org/documentation/consumer/hikey/hikey960/): Hisilicon Kirin 960
    - [HiKey970](https://www.96boards.org/documentation/consumer/hikey/hikey970/): Hi3670
- [Sel4](https://docs.sel4.systems/Hardware/HiKey/)

> Hi6220 V100 integrates the following three MMC modules:
> - MMC0: connectes to eMMC and supports 1-bit, 4-bit, and 8-bit modes.
> - MMC1: connects to the SD 3.0 card and supports 1-bit and 4-bit modes (3V and 1.8V supported for the I/O device).
> - MMC2: connects to the slave device and supports 1-bit and 4-bit modes.
>
> The eMMC/SD core used in Hi6220 is build from Synopsys IP(2.60a). Details about the block can be found in dwc_mobile_storage_db.pdf (which can also be downloaded from https://www.synopsys.com/dw/ipdir.php?c=dwc_mobile_storage).
>
> The base address for MMC0 register is 0xF723_D000.
> The Base address for MMC1 register is 0xF723_E000.
> The Base address for MMC2 register is 0xF723_F000.
>
> --- [Hi6220 Datasheet (`$4.2 SD/SDIO/MMC Host controller`)](https://github.com/96boards/documentation/blob/master/consumer/hikey/hikey620/hardware-docs/Hi6220V100_Multi-Mode_Application_Processor_Function_Description.pdf)

In `edk2-platforms/Platform/Hisilicon/HiKey/HiKey.dsc`:

```
EmbeddedPkg/Universal/MmcDxe/MmcDxe.inf
Silicon/Synopsys/DesignWare/Drivers/DwEmmcDxe/DwEmmcDxe.inf
```

Build the target using the following script:

```
#!/bin/bash

export WORKSPACE=/home/bruin/work/tianocore
export PACKAGES_PATH=$WORKSPACE/edk2:$WORKSPACE/edk2-platforms:$WORKSPACE/edk2-non-osi

pushd $WORKSPACE

rm -rf ./Build/RPi4

source edk2/edksetup.sh

echo "Building BaseTools..."
make -C edk2/BaseTools all

echo "Building firmware for HiKey620..."
GCC5_AARCH64_PREFIX=aarch64-none-linux-gnu- build \
      -n 4 \
      -a AARCH64 \
      -p Platform/Hisilicon/HiKey/HiKey.dsc \
      -t GCC5 \
      -b DEBUG \
      -v -d 9 -j hikey620-build.log \
      -y hikey620-build-report.txt \
      -Y PCD \
      -Y LIBRARY \
      -Y DEPEX \
      -Y HASH \
      -Y BUILD_FLAGS \
      -Y FLASH \
      -Y FIXED_ADDRESS \
      -Y EXECUTION_ORDER \
      all
```

In the build report, we can only find the PCD for the address `0xF723D000` ,which is for `MMC0` (eMMC):

```
4246 gDesignWareTokenSpaceGuid
4247  *M PcdDwEmmcDxeBaseAddress                  :  FIXED   (UINT32) = 0xF723D000 (4146319360)
4248                                                      DEC DEFAULT = 0x0 (0)
4249  *M PcdDwEmmcDxeClockFrequencyInHz           :  FIXED   (UINT32) = 0x5F5E100 (100000000)
4250                                                      DEC DEFAULT = 0x0 (0)
4251     PcdDwEmmcDxeFifoDepth                    :  FIXED   (UINT32) = 0x0 (0)
4252     PcdDwEmmcDxeMaxClockFreqInHz             :  FIXED   (UINT32) = 0x0 (0)
4253  *M PcdDwPermitObsoleteDrivers               :  FIXED  (BOOLEAN) = 1
4254                                                      DEC DEFAULT = 0
```

Searching the web, the following two urls discussed SD/MMC related questions, particulary with DW IP for HiKey:

- [edk2: Question on eMMC and SD driver](https://www.mail-archive.com/edk2-devel@lists.01.org/msg14662.html)
- [DwMmcDxe for HiKey](https://patches.linaro.org/project/uefi_edk2/patch/1534384166-15673-4-git-send-email-haojian.zhuang@linaro.org/)

However, the code from https://git.linaro.org/uefi/linaro-edk2.git is very old and does not contain `DwMmcDxe` driver.

From [Sel4](https://docs.sel4.systems/Hardware/HiKey/), we traced to ` git clone -b hikey --depth 1 https://github.com/96boards/edk2.git linaro-edk2` and a [patch](https://docs.sel4.systems/Hardware/HiKey/edk2.patch).

Patching:

```
cd linaro-edk2
patch -p1 < ~/Downloads/edk2.patch
```

The SD/MMC drivers are listed in `linaro-edk2/HisiPkg/HiKeyPkg/HiKey.dsc`:

```
410   EmbeddedPkg/Universal/MmcDxe/MmcDxe.inf         <= exist in edk2 master: installs binding protocols on driver handle, installs BlockIo protocol on host instance handle
411   EmbeddedPkg/Drivers/DwMmcDxe/DwMmcDxe.inf       <= not in edk2 master: installs gEfiMmcHostProtocolGuid on a new device handle
412   HisiPkg/HiKeyPkg/Drivers/DwSdDxe/DwSdDxe.inf    <= not in edk2 master: installs gEfiMmcHostProtocolGuid on a new device handle
```

To tell the purpose of each driver, search key word `Install`:

- `gBS->InstallMultipleProtocolInterfaces()`, or
- `gBS->InstallProtocolInterface()`, or
- `EfiLibInstallDriverBindingComponentName2()`

to see which interfaces is installed by each driver.

- `EmbeddedPkg/Universal/MmcDxe/MmcDxe.inf`:
    - `Mmc.c:MmcDxeInitialize()`:
        - `EfiLibInstallDriverBindingComponentName2()` installs:
            - `gMmcDriverBinding`
            - `gMmcComponentName`
            - `gMmcComponentName2`
        - `gBS->InstallMultipleProtocolInterfaces()` installs:
            - `gEfiDriverDiagnostics2ProtocolGuid`
    - `Mmc.c:MmcDriverBindingStart()`: in `CreateMmcHostInstance()`, install the following 2 protocols:
        - `gEfiBlockIoProtocolGuid`
        - `gEfiDevicePathProtocolGuid`

```
typedef struct _MMC_HOST_INSTANCE {
  UINTN                     Signature;
  LIST_ENTRY                Link;
  EFI_HANDLE                MmcHandle;
  EFI_DEVICE_PATH_PROTOCOL  *DevicePath;

  MMC_STATE                 State;
  EFI_BLOCK_IO_PROTOCOL     BlockIo;
  CARD_INFO                 CardInfo;
  EFI_MMC_HOST_PROTOCOL     *MmcHost;

  BOOLEAN                   Initialized;
} MMC_HOST_INSTANCE;

typedef struct {
  UINT8 Type;
  UINT8 SubType;
  UINT8 Length[2];
} EFI_DEVICE_PATH_PROTOCOL;

struct _EFI_BLOCK_IO_PROTOCOL {
  UINT64              Revision;
  EFI_BLOCK_IO_MEDIA  *Media;
  EFI_BLOCK_RESET     Reset;
  EFI_BLOCK_READ      ReadBlocks;
  EFI_BLOCK_WRITE     WriteBlocks;
  EFI_BLOCK_FLUSH     FlushBlocks;
};

struct _EFI_MMC_HOST_PROTOCOL {
  UINT32                  Revision;
  MMC_ISCARDPRESENT       IsCardPresent;
  MMC_ISREADONLY          IsReadOnly;
  MMC_BUILDDEVICEPATH     BuildDevicePath;
  MMC_NOTIFYSTATE         NotifyState;
  MMC_SENDCOMMAND         SendCommand;
  MMC_RECEIVERESPONSE     ReceiveResponse;
  MMC_READBLOCKDATA       ReadBlockData;
  MMC_WRITEBLOCKDATA      WriteBlockData;
  MMC_SETIOS              SetIos;
  MMC_ISMULTIBLOCK        IsMultiBlock;
};

typedef enum _MMC_STATE {
    MmcInvalidState = 0,
    MmcHwInitializationState,
    MmcIdleState,
    MmcReadyState,
    MmcIdentificationState,
    MmcStandByState,
    MmcTransferState,
    MmcSendingDataState,
    MmcReceiveDataState,
    MmcProgrammingState,
    MmcDisconnectState,
} MMC_STATE;

typedef struct {
  UINT16    RCA;
  CARD_TYPE CardType;
  OCR       OCRData;
  CID       CIDData;
  CSD       CSDData;
  ECSD      *ECSDData;                         // MMC V4 extended card specific
} CARD_INFO;

typedef enum {
  UNKNOWN_CARD,
  MMC_CARD,              //MMC card
  MMC_CARD_HIGH,         //MMC Card with High capacity
  EMMC_CARD,             //eMMC 4.41 card
  SD_CARD,               //SD 1.1 card
  SD_CARD_2,             //SD 2.0 or above standard card
  SD_CARD_2_HIGH         //SD 2.0 or above high capacity card
} CARD_TYPE;
```

call stack of `Mmc.c:MmcDxeInitialize()`:

```
MmcDxeInitialize()
|-- InitializeMmcHostPool()
|   `-- InitializeListHead(&mMmcHostPool)
|-- EfiLibInstallDriverBindingComponentName2()
|-- InstallMultipleProtocolInterfaces()
|-- gBS->CreateEvent(EVT_TIMER, checkCardsCallback...)
`-- gBS->SetTimer(TimerPeriodic, 200ms)
```



## BlueField?

- [how to get BlueField software?](https://community.mellanox.com/s/article/How-to-Get-BlueField-Software)
- [BlueField-2.0.0.10829.tar.xz (~600M)](http://www.mellanox.com/downloads/BlueField/BlueField-2.0.0.10829/BlueField-2.0.0.10829.tar.xz)

The downloaded `BlueField-2.0.0.10829` contains src for ATF/EDK2/Kernel.

## ???

Device drivers:

- `edk2/MdeModulePkg/Bus/Sd/SdDxe`: seems that this requires `EFI_SD_MMC_PASS_THRU_PROTOCOL`
- `EmbeddedPkg/Universal/MmcDxe/MmcDxe.inf`: seems no pass-through protocol required

```
bruin@u2004 ~/work/tianocore $ find . -type f -name "*.dsc" -exec grep -Hn SdDxe.inf {} \;
./edk2/UefiPayloadPkg/UefiPayloadPkg.dsc:599:  MdeModulePkg/Bus/Sd/SdDxe/SdDxe.inf
./edk2/MdeModulePkg/MdeModulePkg.dsc:248:  MdeModulePkg/Bus/Sd/SdDxe/SdDxe.inf
./edk2-platforms/Platform/Intel/Vlv2TbltDevicePkg/PlatformPkgIA32.dsc:1139:  MdeModulePkg/Bus/Sd/SdDxe/SdDxe.inf
./edk2-platforms/Platform/Intel/Vlv2TbltDevicePkg/PlatformPkgX64.dsc:1154:  MdeModulePkg/Bus/Sd/SdDxe/SdDxe.inf
./edk2-platforms/Platform/Intel/WhiskeylakeOpenBoardPkg/UpXtreme/OpenBoardPkg.dsc:359:  MdeModulePkg/Bus/Sd/SdDxe/SdDxe.inf
```

Adding `MdeModulePkg/Bus/Sd/SdDxe/SdDxe.inf` into `MyChip.dsc` without any other changes: build ok without error! In the build report, no PCD for register address. Seems that this is a device driver (i.e. not bus driver) for devices supports `EFI_SD_MMC_PASS_THRU_PROTOCOL`.
