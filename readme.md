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
connect via VNC. Example: 192.168.1.154:1


