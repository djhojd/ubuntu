# Extra Mouse Buttons

http://askubuntu.com/a/246849/41705



You're going to need several applications for this, to install them run

sudo apt-get install xbindkeys xautomation xev  

Step 1

You need to find the button numbers for the buttons on your mouse. Run xev. You will see a litle white windows appear, put your mouse in it and press your mouse buttons (it's best to do this one button at a time). You should get output like this for each button:

ButtonRelease event, serial 41, synthetic NO, window 0x4c00001,
root 0x2e9, subw 0x4c00002, time 25804905, (31,28), root:(821,80),
state 0x110, button 1, same_screen YES

(note: xev also capture mouse movement so you might need to sift through mouse movement events to find your button events; e.g.: xev -event mouse | grep Button --before-context=1 --after-context=2)

This is what is important from that output: button 1. That tells us that particular button is button one. I would store this in a .txt file for now.
Step 2

Create the xbindkeys config file using:

xbindkeys --defaults > $HOME/.xbindkeysrc  

Next we need to add the key/button bindings to the config file. You can open this file with gedit $HOME/.xbindkeysrc. This is where the fun begins. We are going to use xte to set bindings to our buttons.

To make a button act as Ctrl we would add:

"xte 'key Control_L'"
b:1  

This would bind Ctrl to mouse button one.

If you will tell me the button numbers of your buttons and what you want each to do, I will write the script for you.
