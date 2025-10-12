# Boogatti
Let me preface this with saying that I am a tinkerer electrician, not a pro coder or electrical engineer.

This is my first time writing a README/tutorial, so forgive me if I don't follow any norms.

This project began with my wife getting a great deal on a used Power Wheels Cars. 
Like this one: https://foter.com/products/vintage-style-power-wheels-car

It did not come with a remote and she wanted me to get one and get it working so she could drive it around with Halloween props.
I'll be honest, in hindsight, I bought a bunch of unecesssary crap.
I bought a full wire harness, remote, and controller replacement kit. 
I figured this would save time with trying to figure out a different remote.
It did not. The wire harness sort of matched up but not really. 
I applied power to the new controller on my workbench and somehow, miraculiosly, was able to pair the very poor quality remote.
The whole thing was junk. I can't believe they even sell this stuff for more than 30 bucks new.

Anyways...I had a bluetooth 8bitdo NES controller already so I figured what the hell, I'll program a raspberry pi, add a few relays, 
a speaker, and some audio files to trick this thing out. I have a bit of experience with using Node-Red so I started looking for in the palette. To my surprise I could not find a module to work. Everything is ble. I was able to connect, pair, and trust through bluetoothctl, but could not figure out how to get any button data. This was beyond me.  I then threw some money at Amazon and ordered a Radiolink T8S 8 Channels 2.4GHz RC Pocket Size Portable Transmitter and Receiver R8EF RX.
I followed the instructions and videos here: https://www.reddit.com/r/raspberry_pi/comments/sp8etb/radio_controlled_raspberry_pi_over_sbus/.
I ended up getting some data on my pi4b but I would only get it once upon connection, but not a continuous stream. I figured since the radio receivers weren't exactly the same, that was probably my problem.

At this point, I've spent way too much on this yard sale car, but I figured I might learn something and possible use the parts for a different project. I try one more time, and pick up a "2 Pack Wireless SNES Controller, LUXMO 2.4GHz USB Gamepad Classic Game Controller" from Walmart.
Again, I didn't really know how I'm going to get data out of this but I felt like I was getting closer. I end up stumbling upon this post: https://forums.linuxmint.com/viewtopic.php?t=427214. The evtest was the missing piece of the puzzle. The xbox stuff listed on that thread is not relevant.
And the rest was basically a cake walk.

Parts needed:
1. Raspberry Pi- I used the 4b : https://a.co/d/7QaD7z5
2. Relays : I ended up using 3 of these relay pairs : https://a.co/d/6uRmdw6

  1 pair for steering - 2 relays that reverse 12vdc polarity to switch between left and right - common terminals go to motor leads

  1 pair for drive - 2 relays that reverse 12vdc polarity to switch between forward and reverse - common terminals go to motor leads

  1 pair for lights and optional props

3. Dewalt battery adapter : https://a.co/d/8VYDHKD
4. 20v to 12v power adapter with fuse : https://a.co/d/guRQAic
5. 12v to 5v power adapter for pi power : https://a.co/d/e88wEeP
6. usb c switch for pi power : https://a.co/d/ieMOwG9
7. pi pin splitter : https://a.co/d/iIvIKLA
8. wire terminal blocks : https://a.co/d/8Z5sAMk
9. misc crimps and wires. I found these to be helpful for terminating : https://a.co/d/9YM4AUJ

Stuff to install on the pi4b:
1. operating system : I used RASPBERRY PI OS LITE (64-BIT)
2. Node-Red : https://nodered.org/docs/getting-started/raspberrypi
    - modules needed
        -node-red-contrib-ui-joystick     this will also allow you to control things via a Node-Red dashboard
        -node-red-node-pi-gpio            can be installed during Node-Red install
3. amixer - to control volume : sudo apt install alsa-utils
4. mplayer - needed to play audio : sudo apt install mplayer
5. evtest - needed to capture controller events  : sudo apt install evtest
   - when using evtest, you must identify your event# and either move the usb dongle to a different port to match the code (event0) or change the code to match your         event#.  The event number corresponds to the usb port(not literal port #) that the SNES controller dongle is plugged in to. If you move it or it doesn't              match up, the controller won't work.

If stuff doesn't work:

  -check rasp-gpio pin numbers

  -check evtest event#

  -check contoller button mapping

  -if motor operation doesn't match button pushed, reverse motor lead wires

  -check audio folder location. should be in .node-red/

  wiring pics:

  https://drive.google.com/file/d/1dMyVkAzstIFU-WFvzVmFTmKbLRs9nuQs/view?usp=drive_link

  https://drive.google.com/file/d/1L3-065Ip2qIkVzgB_pMS6Q5aZIJ-u1QE/view?usp=drive_link


