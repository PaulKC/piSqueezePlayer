# piSqueezePlayer
Small 3D printed squeezebox player based on a Raspberry Pi

## BOM
* Raspberry Pi Zero W
* HiFiBerry MiniAMP
* 2" Inch 4Ohm 3W Speaker [https://www.aliexpress.com/item/32593991938.html?spm=a2g0s.9042311.0.0.6a994c4d6uO0Mn](Link)
* Rotary encoder
* 8x M3 ca. 18mm
* 8x M3 ca. 5mm
* 8x M3 Nut

## Software
* piCorePlayer [https://www.picoreplayer.org/]
* SqueezeButtonPi-Daemon [https://github.com/coolio107/SqueezeButtonPi-Daemon]

### Installation
* In the piCorePlayer webgui select "Advanced" on the bottom of the main page.
* Install the extension pcp-sbpd.tcz
* In the Squeezelight Tab, select HiFiBerry DAC Zero/MiniAMP as audio output device
* Create a executable file `/home/tc/sbpd-script.sh` with the content:
```#!/bin/sh

# start pigpiod daemon
pigpiod -t 0 -f -l -s 10

# wait for pigpiod to initialize - indicated by 'pigs t' exit code of zero
count=10 # approx time limit in seconds
while ! pigs t >/dev/null 2>&1 ; do
        if [ $((count--)) -le 0 ]; then
                printf "\npigpiod failed to initialize within time limit\n"
                exit 1 # or however you want to deal with failure
        fi
#       printf "\nWaiting for pigpiod to initialize\n"
        sleep 1
done
printf "\npigpiod is running\n"

# load uinput module - required to be able to send keystrokes
# then set the permission to group writable, so you don't need to run sbpd with
sudo modprobe uinput
sudo chmod g+w /dev/uinput

# issue the sbpd command
sbpd e,22,27,VOLU b,26,PLAY -d
```
* Backup the configuration in the Main Page
* Under Tweaks add the command `/home/tc/sbpd-script.sh` to user commands. (Pin numbers depend on setup)