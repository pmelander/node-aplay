node-aplay
===========

ALSA aplay wrapper for Node.js

Installation
-----------
### Debian/Ubuntu ###

#### Get ready ####

Before we start the real work, please update the system.
````
sudo apt-get update
sudo apt-get upgrade
````
Install ALSA for audio playback
````
sudo apt-get install alsa-base alsa-utils
````

Example Usage
------------

````javascript
var Sound = require('node-aplay');

// fire and forget:
new Sound('/path/to/the/file/filename.mp3').play();

// with ability to pause/resume:
var music = new Sound('/path/to/the/file/filename.mp3');
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
