Retrogame2PlayersB+
===================

Raspberry Pi GPIO-to-USB utility for classic game emulators.

Installation
============

Now we have configure to allow retrogame to work and be launched at startup. As in http://learn.adafruit.com/retro-gaming-with-raspberry-pi/buttons, you make

Retrogame requires the uinput kernel module. This is already present on the system but isn't enabled by default. For testing, you can type:

````
sudo modprobe uinput
````

To make this persistent between reboots, append a line to /etc/modules (or edit the file) :

````
sudo sh -c 'echo uinput >> /etc/modules'
````

Now we're in good shape to test it! Retrogame needs to be run as root (need access to memory), i.e.:

````
sudo ./retrogame
````

Give it a try. If it seems to be working, press control+C to stop the program and we'll then set up the system to launch this automatically in the background at startup.

````
sudo nano /etc/rc.local
````

Before the final "exit 0" line, insert this line:

````
/home/pi/Retrogame-2players/retrogame &

````
If you placed the software in a different location, this line should be changed accordingly. "sudo" isn't necessary here because the rc.local script is already run as root.

Reboot the system to test the startup function:

````
sudo reboot
````

The software will now be patiently waiting in the background, ready for use with any emulators.

Each emulator will have its own method for configuring keyboard input. Set them up so the keys match your controller outputs. Up/down/left/right from the arrow keys is a pretty common default among these programs, but the rest will usually require some tweaking.


