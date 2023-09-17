# padavan-4.4 #

该项目基于原始的rt-n56u，具有最新的mtk 4.4.198内核，该内核是从D-LINK GPL代码获取的。

- 特点
  - 基于4.4.198 Linux内核
  - 支持基于MT7621的设备
  - 支持MT7615D/MT7615N/MT7915D无线芯片
  - 使用legacy驱动程序支持raeth和mt7621 hwnat
  - 支持qca快捷键-fe
  - 支持基于netfilter的IPv6 NAT
  - 支持内核集成WireGuard
  - 支持fullcone NAT（由Chion82提供）
  - 支持通过sysfs控制LED&GPIO

- WIP
  - 802.11kvr和mtkiappd漫游功能
  - IPTV相关功能

- 支持的设备
  - CR660x
  - JCG-Q20
  - JCG-AC860M
  - JCG-836PRO
  - JCG-Y2
  - JDC-1
  - DIR-878
  - DIR-882
  - K2P
  - K2P-USB
  - NETGEAR-BZV
  - MR2600
  - MI-R3P
  - XY-C1
- 编译步骤
  - 安装依赖项
    ```sh
    # Debian/Ubuntu
    sudo apt install unzip libtool-bin curl cmake gperf gawk flex bison nano xxd \
        fakeroot kmod cpio git python3-docutils gettext automake autopoint \
        texinfo build-essential help2man pkg-config zlib1g-dev libgmp3-dev \
        libmpc-dev libmpfr-dev libncurses5-dev libltdl-dev wget libc-dev-bin

    # Archlinux/Manjaro
    sudo pacman -Syu --needed git base-devel cmake gperf ncurses libmpc \
            gmp python-docutils vim rpcsvc-proto fakeroot cpio help2man

    # Alpine
    sudo apk add make gcc g++ cpio curl wget nano xxd kmod \
        pkgconfig rpcgen fakeroot ncurses bash patch \
        bsd-compat-headers python2 python3 zlib-dev \
        automake gettext gettext-dev autoconf bison \
        flex coreutils cmake git libtool gawk sudo
    ```
  - 克隆源码
    ```sh
    git clone https://github.com/Tine789/rt-n56u.git
    ```
  - 准备工具链
    ```sh
    cd padavan-4.4/toolchain-mipsel

    # (Recommend) Download prebuilt toolchain for x86_64 or aarch64 host
    ./dl_toolchain.sh

    # or build toolchain with crosstool-ng
    # ./build_toolchain
    ```
  - 修改模板文件并开始编译
    ```sh
    cd padavan-4.4/trunk

    # (Optional) Modify template file
    # nano configs/templates/K2P.config

    # Start compiling
    fakeroot ./build_firmware_modify K2P

    # To build firmware for other devices, clean the tree after previous build
    ./clear_tree
    ```

- 手册
  - Controlling GPIO and LEDs via sysfs
  - How to use NAND RWFS partition
  - How to use IPv6 NAT and fullcone NAT
  - How to add new device support with device tree
