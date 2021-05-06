# Headless Raspberry Pi SSH & VNC setup

## Step 1
Download latest raspbian version and flash SD card.


## Step 2
enable SSH
```sh
touch /Volumes/boot/ssh
```

## Step 3
add Wifi configuration
```sh
nano /Volumes/boot/wpa_supplicant.conf
```

insert this:

```sh
country=US
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
	ssid="[SSID]"
	psk="[password]"
}
```


## Step 4
Insert SD card into Raspberry Pi. If you receive EHSA error when connecting, type this:
```sh
ssh-keygen -R [IP of Pi]
```

## Step 5
When connected to Pi type this:
```sh
sudo apt update
sudo apt install realvnc-vnc-server realvnc-vnc-viewer
```

## Step 6
Enable VNC in raspi-config under interfacing
```sh
sudo raspi-config
```

## Step 7
install tightvncserver
```sh
sudo apt install tightvncserver
```

## Step 8
create ./vnc
```sh
sudo nano ./vnc
```
add this to it
```sh
#!/bin/sh

vncserver -geometry 1920x1080
```

## Step 9
make it executable:
```sh
sudo chmod +x ./vnc
./vnc
```

## Step 10
enable copy paste over vnc

```sh
sudo apt-get install autocutsel
```

```sh
cd .vnc/
nano xstartup
```

add this to xstartup file:

```sh
#!/bin/sh

xrdb $HOME/.Xresources
xsetroot -solid grey
autocutsel -fork
#x-terminal-emulator -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &
#x-window-manager &
# Fix to make GNOME work
export XKL_XMODMAP_DISABLE=1
/etc/X11/Xsession
```

## Step 11
connect via VNC. Example: 192.168.1.154:1

Useful Links:

Install Python3.9
https://community.home-assistant.io/t/python-3-9-install-on-raspberry-pi-os/241558

https://installvirtual.com/install-python-3-7-on-raspberry-pi/

https://superuser.com/questions/1496683/upgrade-pip-to-newest-version-on-ubuntu-16-04
