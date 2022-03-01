# AndroidLearning
Learning Android

# Build AOSP(WSL)
## Setup workstation
Run below command
```
sudo apt-get install git-core gnupg flex bison build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z1-dev libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig
sudo apt install libncurses5
sudo ln -s /usr/bin/python3 /usr/bin/python
```
## Install repo and gain credentials to all git repositories
Download the Repo Launcher and ensure that it's executable:
```
sudo wget 'https://storage.googleapis.com/git-repo-downloads/repo' -P /usr/local/sbin/
sudo chmod a+x /usr/local/sbin/repo
```
## Initialize and sync the code

I do not recommend using dirs under /mnt, which causes a lot of problems. Use filesystem inside WSL instead.
```
git config --global user.email mmx@microsoft.com
git config --global user.name mmx
```
Initialize the AOSP repository source code，do not do it with sudo
```
repo init -u  https://android.googlesource.com/platform/manifest -b android-12.0.0_r32
```
Sync code
Run command: 
```
repo sync
```
This may take a long time

## Ubuntu memory
### The default memory of WSL is 8 G and it is not enough for building.
Create .wslconfig in C:\user\<username>\.wslconfig and added below content:
```
[wsl2]
processors=8
memory=12GB
swap=20GB
```
memory must be greater than 12 GB, otherwise it would be failed while buding metalava. 
swap must be greater than 10 GB, otherwise it would be failed while build soong. 

```
sudo swapoff -a
sudo dd if=/dev/zero of=/swapfile bs=1G count=32 status=progress
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
sudo swapon --show
free -h 
```

## Building
```
source build/envsetup.sh
lunch aosp_oriole-userdebug
m
```
