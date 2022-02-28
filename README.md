# AndroidLearning
Learning Android

# Build AOSP(WSL)
## Setup workstation
Run below command
```
sudo apt-get install git-core gnupg flex bison build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z1-dev libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig
sudo apt install libcurses5
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
