# install-guest-additions.md

## REsrouces

* Download 

## Install

### Manual update to latest stable version

#### Determin latest stable version

```shell
wget http://download.virtualbox.org/virtualbox/LATEST-STABLE.TXT
cat LATEST-STABLE.TXT
```

output example:

```shell
5.2.12
```

#### Download latests stable 

```shell
mkdir -p ~/iso/virtualbox/5.2.12
cd ~/iso/virtualbox/5.2.12
wget http://download.virtualbox.org/virtualbox/5.2.12/VBoxGuestAdditions_5.2.12.iso
```

copy to host location

```shell
sudo cp ~/iso/virtualbox/5.2.12/VBoxGuestAdditions_5.2.12.iso /usr/share/virtualbox/.
sudo chmod 0644 /usr/share/virtualbox/VBoxGuestAdditions_5.2.12.iso 
sudo ls -al /usr/share/virtualbox/
```

### Prepare VM in VirtualBox GUI

* Halt all VirtualBoxes (or other VM's)
* Open the VurtualBox GUI Interface
* Choose **File** > **Virtual Media Manager**
* Choose the **Optical disks** tab.
  * If you already see **VBoxGuestAdditions.iso** select it and remove it if it is pointing to an old version.

### Prepare the VM

* Select the VM
* Choose **Storage** 
* Ensure that you have an **IDE Controller**
* Ensure you have an **Optical Drive** on the controller, if not add one and choose **Choose Image**, brows to /usr/share/virtualbox and then select the ISO you want (The latest version).
* You can do the same for any other VM's
* Start the VM's using vagrant



## Check for

```shell
lsmod | grep -i vbox
```

```shell
vboxpci                24576  0
vboxnetadp             28672  0
vboxnetflt             28672  1
vboxdrv               471040  4 vboxnetadp,vboxnetflt,vboxpci
```

### the Debian way

install ubuntu virtualbox-guest-additions-iso package


```shell
sudo apt install virtualbox-guest-additions-iso
```

Confirm that ISO is now available on host

```shell
ls -al /usr/share/virtualbox/
```

## On VM

* Start VM
* go to Devices -> Insert Guest Additions CD image to mount the ISO image.
* From the terminal run:

### Precise

```shell
sudo su -
apt-get update
apt-get source linux-image-$(uname -r)
apt-get install build-essential
mkdir -p /media/cdrom
mount /dev/cdrom /media/cdrom
#/media/cdrom/VBoxLinuxAdditions.run
/media/cdrom/VBoxLinuxAdditions.run --nox11
reboot
```

### xenial

```shell
sudo su -
apt update
apt install build-essential
apt install linux-header-$(uname -r)
apt install gcc make
mkdir -p /media/cdrom
mount /dev/cdrom /media/cdrom
# /media/cdrom/VBoxLinuxAdditions.run
/media/cdrom/VBoxLinuxAdditions.run --nox11
reboot
```

After reboot:

```shell
# sudo usermod --append --groups vboxsf USERNAME
sudo usermod --append --groups vboxsf vagrant

```

Host shares should now be mounted in Ubuntu guest under /media via the installed VBoxService service, set to start on system boot-up.

## 

