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
* Under Tweaks add the command "sbpd e,22,27,VOLU b,26,PLAY" to user commands. (Pin numbers depend on setup)