# Background:
Notes from 7-1-16 call w/ @samatt, @davemayers, @daveriordan about how to set up `sniffer_build` on a Raspberry Pi

# Call Notes:


need sniffer source; wrapper around c

build.sh script inside sniffer_source

Used wheezy and pwnpi; compiled for wheezy

Recently did a Pi project at MOOGfest

Is pi connected to internet? Has access. Needs connection to internet

Relies on developer version of libpcap-dev

`sudo apt-get install libpcap-dev`

Then run build.sh

tons.h doesn't exist

now we're in main.cpp
* "tins/tins.h" ; bah not working
* chek for lib/lbitins/

Downloading the other file

Need to delete this lib folder, it'll reinstall for the pi


How's the binary compiled?

Checks for libtins on the computer; if so, builds the sniffer. If not, downloads libtins binary from Surya's compiled libtins and then builds the sniffer

after line 49, the g++ line compiles the app

Makes a new directory called lib and everything works around that

This build.sh creates an excecutable and thats all thats there

running the excecutable should just be able to output this to a stream; can run it to a file.

Only things to be aware of on pi:
* which wifi to use?
 * TP Link WN722N
 * Most important thing is a card that lets you set the frequency + set the card into monitor mode
 * Use this chipset: https://wikidevi.com/wiki/Atheros_AR9271
 * will need to:
    * NSHEY is limited (even for mac) all wifi hopping is handled to hardcode mac commands (airport commands)
    * NEEDS to use iwconfig to hop
        * iwconfig wlan0 channel 
        * iwconfig wlan0 channel channel_num
        * If having troupble setting it into monitor mode, install aircrack, use airmon_ng, and just run airmon
        * airmon lets you run the frequency channel
    * Run airmon ahead of it
    * Write a python script to spawn a child process for airmon, spawn a process for sniffer, run a timer
    * LOOP: airmon channel hop [1,6,11], sniff, sleep(5000), kill sniff, airmon channel hop REPEAT


TESTING THE PROCESS:
* Delete the binary
* Delete the lib folder

