node-aplay
===========

ALSA aplay wrapper for Node.js

This module was initially intended to provide basic audio capabilities in the Raspbian distribution of Debian on a Raspberry Pi platform. Node-aplay should however work on any Debian/Ubuntu system providing ALSA support has been installed.

ALSA stands for Advanced Linux Sound Architecture. It is a suite of hardware drivers, libraries and utilities which provide audio and MIDI functionality for the Linux operating system.

aplay is a simple native ALSA wav player.

Installation
-----------
### Debian/Ubuntu/Raspbian ###

#### Get ready ####

Before we start the real work, please update the system.
````
sudo apt-get update
sudo apt-get upgrade
````
If you are running on Raspberry Pi, please update Raspbian
````
sudo rpi-update
````

Install ALSA for audio playback
````
sudo apt-get install alsa-base alsa-utils
````

#### USB Audio on Raspberry Pi ####
If you are planning on using a USB audio on Raspberry Pi you will need to set your USB audio device as the default device.

Edit /etc/modprobe.d/alsa-base.conf and replaced the line:
````
options snd-usb-audio index=-2
````
With the followin lines:
````
options snd-usb-audio index=0 nrpacks=1
options snd-bcm2835 index=-2
````

After a reboot of your Raspberry Pi
````
aplay -l
````
Should output the following:
````
**** List of PLAYBACK Hardware Devices ****
card 0: XXXX [XXXX], device 0: USB Audio [USB Audio]
Subdevices: 1/1
Subdevice #0: subdevice #0
````

Your device volume will be set to 0 by default. Use the ALSA mixer to adjust the volume using your arrow keys:
````
alsamixer
````

Example Usage
------------

````javascript
var Sound = require('node-aplay');

// fire and forget:
new Sound('/path/to/the/file/filename.wav').play();

// with ability to pause/resume:
var music = new Sound('/path/to/the/file/filename.wav');
music.play();

setTimeout(function () {
	music.pause(); // pause the music after five seconds
}, 5000);

setTimeout(function () {
	music.resume(); // and resume it two seconds after pausing
}, 7000);

// you can also listen for various callbacks:
music.on('complete' function () {
	console.log('Done with playback!');
});
````

It's simple as that.

Documentation
------------
In progress.
