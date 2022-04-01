# SnapBack Kernel
## Description
The SnapBack Kernel is a custom build of the stock T870XXU2BUI1 kernel from Samsung for the Tab S7 WIFI SM-T870 (GTS7LWIFI) Tablet. This kernel was built for use with Kail NetHunter.
## Features
### Changes 
- Selinux toggleable
- TCP Westwood: congestion control
### Added
- [Support for 24 Bit Audio](https://github.com/Bruce303lee/android_kernel_samsung_sm8250/commit/bd5cbcfcd3e0d85a574467d173bb77b1071ab76f)
- [Bluetooth Drivers](https://github.com/Bruce303lee/android_kernel_samsung_sm8250/commit/64d9a6042ad8f09ec9440040331818855550697c)
- [RFCOMM Protocol](https://github.com/Bruce303lee/android_kernel_samsung_sm8250/commit/64d9a6042ad8f09ec9440040331818855550697c)
- [MAC80211](https://github.com/Bruce303lee/android_kernel_samsung_sm8250/commit/adec45e493b3cfeef0b21f5aedcc533d9645c6c1)
- [SDR Support](https://github.com/Bruce303lee/android_kernel_samsung_sm8250/commit/d7a5cd864916f896ddd0027b6c2cc79aeedc2975)
- [USB OTG](https://github.com/Bruce303lee/android_kernel_samsung_sm8250/commit/cbe471335a1611b8846ca0f9ff2cf0c693287a86)
- [CD-ROM/DVD Filesystems](https://github.com/Bruce303lee/android_kernel_samsung_sm8250/commit/9f7aac14496507f11c14cc584a838ddd8d0e8206)
- [USB NET RNDIS WIFI/HOST](https://github.com/Bruce303lee/android_kernel_samsung_sm8250/commit/ee56c3c34698ce83fc90bdc90cbe12fb90d6446e)
### Disabled
- [Android Paranoid Network](https://github.com/Bruce303lee/android_kernel_samsung_sm8250/commit/e673b27c4ff33cc31641d007c88a478fbd41f841)
- [Module Signature Verification](https://github.com/Bruce303lee/android_kernel_samsung_sm8250/commit/0c99dc3ff3f481470faccde4ec475479dde0611e)
- [KNOX NCM](https://github.com/Bruce303lee/android_kernel_samsung_sm8250/commit/676530354696ef0891a0104e4b37cca265526421)
- [DEFEX](https://github.com/Bruce303lee/android_kernel_samsung_sm8250/commit/af80a1fa7b73c7db983ab874287ab88ac62cf24e)
- [DSMS](https://github.com/Bruce303lee/android_kernel_samsung_sm8250/commit/af80a1fa7b73c7db983ab874287ab88ac62cf24e)
- [FIVE](https://github.com/Bruce303lee/android_kernel_samsung_sm8250/commit/af80a1fa7b73c7db983ab874287ab88ac62cf24e)
- [GAF](https://github.com/Bruce303lee/android_kernel_samsung_sm8250/commit/af80a1fa7b73c7db983ab874287ab88ac62cf24e)
- [UH](https://github.com/Bruce303lee/android_kernel_samsung_sm8250/commit/e6fed3baa75899f93410af3105effcee95114d2e)
## Setup
### Environment
Virtual Box VM running Kali Linux 2021.4a
#### _Specs_
- 16 GB RAM
- 8 Cores
- Bridged networking for SSH + XRDP
- 200 GB Drive Space

### Sorcery
- [Android NDK r21](https://dl.google.com/android/repository/android-ndk-r21e-linux-x86_64.zip)
- [Qualcomm Toolchain v8](https://developer.qualcomm.com/software/snapdragon-llvm-compiler-android/tools)
- [Samsung Kernel Source](https://opensource.samsung.com/uploadSearch?searchValue=SM-T870)
 
### Dev Ops
#### Directory structure
We will create the following directory structure
```sh
~/android/kernel/toolchain/standalone
```
Download the modified kernel source
```sh
sudo apt install git wget
mkdir ~/android
cd ~/android
git clone https://github.com/Bruce303lee/android_kernel_samsung_sm8250
mv android_kernel_samsung_sm8250 kernel
```
#### Download and extract the NDK 
```sh
mkdir ~/toolchains
cd ~/toolchains
wget https://dl.google.com/android/repository/android-ndk-r21e-linux-x86_64.zip
unzip android-ndk-r21e-linux-x86_64.zip
```
#### Extract the Qualcomm Toolchain
```sh
cd android-ndk-r21e/
tar -zxf ../snapdragon-llvm-8.0.6-linux64.tar.gz
```
#### Make Standalone SnapDragon Toolchain
```sh
cd build/tools  
python make_standalone_toolchain_snapdragon_llvm.py --arch arm64 --api 30 --install-dir=~/android/kernel/toolchain/standalone
```
#### Install packages
```sh
sudo apt install bison flex libssl-dev bc
```
#### Downgrade python
To continue the build past instrumenting vmlinux... we need to downgrade python.
```sh 
sudo rm /usr/bin/python
sudo ln /usr/bin/python2.7 /usr/bin/python
```
#### Compile the kernel
```sh
cd ~/android/kernel
./build_kernel.sh
```
## Thanks
|Git User|Contribution|
|------|------|
|[ianmacd](https://github.com/ianmacd) | [TWRP](https://github.com/TeamWin/Team-Win-Recovery-Project) |
|[b1ad3runn3r](https://github.com/b1ad3runn3r)  | [drag-kernel](https://github.com/b1ad3runn3r/drag-kernel-t975) |
|[Official-Ayrton990](https://github.com/Official-Ayrton990) | [Quantic Kernel](https://github.com/Official-Ayrton990/android_kernel_samsung_sm8250.git) |

## _By Bruce303Lee - 3-31-2022_
