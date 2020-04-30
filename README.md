# Instructions for building the fip files for mainline u-boot for the Hardkernel ODroid N2 board

Note: This build was done on Ubuntu 18.04.4 LTS
First, login as a normal user (this assumes a clean install of Ubuntu 18.04.4 LTS)
~~~~~
sudo apt install git libc6-i386
sudo apt install libstdc++6:i386 zlib1g:i386
mkdir odroidn2
cd ordoidn2
wget https://releases.linaro.org/archive/13.11/components/toolchain/binaries/gcc-linaro-aarch64-none-elf-4.8-2013.11_linux.tar.xz
wget https://releases.linaro.org/archive/13.11/components/toolchain/binaries/gcc-linaro-arm-none-eabi-4.8-2013.11_linux.tar.xz
tar xvfJ gcc-linaro-aarch64-none-elf-4.8-2013.11_linux.tar.xz
tar xvfJ gcc-linaro-arm-none-eabi-4.8-2013.11_linux.tar.xz
export PATH=$PWD/gcc-linaro-aarch64-none-elf-4.8-2013.11_linux/bin:$PWD/gcc-linaro-arm-none-eabi-4.8-2013.11_linux/bin:$PATH
git clone --depth 1 https://github.com/hardkernel/u-boot.git -b odroidn2-v2015.01 odroid-u-boot
cd odroid-u-boot
make odroidn2_defconfig
make
mkdir fip-bin
wget https://github.com/BayLibre/u-boot/releases/download/v2017.11-libretech-cc/blx_fix_g12a.sh -O fip-bin/blx_fix.sh
cp build/scp_task/bl301.bin fip-bin/
cp build/board/hardkernel/odroidn2/firmware/acs.bin fip-bin/
cp fip/g12b/{bl2.bin,bl30.bin,bl31.img,ddr3_1d.fw,ddr4_1d.fw,ddr4_2d.fw} fip-bin/
cp fip/g12b/{diag_lpddr4.fw,lpddr4_1d.fw,lpddr4_2d.fw,piei.fw,aml_ddr.fw} fip-bin/
cp fip/g12b/aml_encrypt_g12b fip-bin
~~~~~
The contents of fip-bin are what are commited to this repository.