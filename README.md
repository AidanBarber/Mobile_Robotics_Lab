# Mobile_Robotics_Lab

## Wifi Setup
Run the Following in terminal:
```
sudo apt update
sudo apt upgrade
sudo apt install git build-essential dkms
sudo reboot
git clone https://github.com/cilynx/rtl88x2bu
cd rtl88x2bu/
sed -i 's/I386_PC = y/I386_PC = n/' Makefile
sed -i 's/ARM_RPI = n/ARM_RPI = y/' Makefile
VER=$(sed -n 's/\PACKAGE_VERSION="\(.*\)"/\1/p' dkms.conf)
sudo rsync -rvhP ./ /usr/src/rtl88x2bu-${VER}
sudo dkms add -m rtl88x2bu -v ${VER}
sudo dkms build -m rtl88x2bu -v ${VER} # Takes ~3-minutes on a 3B+
sudo dkms install -m rtl88x2bu -v ${VER}
sudo modprobe 88x2bu
```
Plug in the USB. Take out the sd card and edit the wifi netplan file like normal. Add a new section for the new adapter as wlan1 similar to wlan0. It should look similar to something below.
```
  wifis:
    wlan0:
      dhcp4: yes
      dhcp6: yes
      access-points:
    wlan1:
      dhcp4: yes
      dhcp6: yes
      access-points:
        Mobile Robotics:
          password: <password here>
```
