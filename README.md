Retrogame2PlayersB+
===================

Raspberry Pi GPIO-to-USB utility for classic game emulators.

Compilation
===========

````
$ git clone https://github.com/n-i-x/Raspicade-Retrogame-2Player-BPlus.git
$ cd Raspicade-Retrogame-2Player-BPlus
$ make
````

Pinout Mapping
==============

````
Player 1 :
GPIO 02 -> KEY_UP       // Up
GPIO 03 -> KEY_DOWN     // Down
GPIO 04 -> KEY_LEFT     // Left Joystick
GPIO 14 -> KEY_RIGHT    // Right
GPIO 15 -> KEY_LEFTCTRL // Button 1
GPIO 17 -> KEY_LEFTALT  // Button 2
GPIO 24 -> KEY_SPACE    // Button 3
GPIO 18 -> KEY_LEFTSHIFT// Button 4
GPIO 27 -> KEY_Z        // Button 5
GPIO 22 -> KEY_X        // Button 6
GPIO 10 -> KEY_C        // Button 7
GPIO 23 -> KEY_5        // Button 8
GPIO 09 -> KEY_1        // Button Start P1
GPIO 25 -> KEY_3        // Button Coins/Credits P1

GPIO 08 -> KEY_0        // Button to Halt System -> "sudo halt" is launched
````

Holding Start P1 + Coins/Credits P1 for more than 1 second will produce "KEY_ESC" (Escape Key).

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
/home/pi/Raspicade-Retrogame-2Player-BPlus/retrogame &

````
If you placed the software in a different location, this line should be changed accordingly. "sudo" isn't necessary here because the rc.local script is already run as root.

Reboot the system to test the startup function:

````
sudo reboot
````

The software will now be patiently waiting in the background, ready for use with any emulators.

Each emulator will have its own method for configuring keyboard input. Set them up so the keys match your controller outputs. Up/down/left/right from the arrow keys is a pretty common default among these programs, but the rest will usually require some tweaking.

Arcade Wiring
=============

See https://github.com/ian57/Raspicade-Retrogame-2Player-BPlus/wiki
