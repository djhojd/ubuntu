# Mouse Bind Keys

Hi everybody,

 

Just for people looking for linux options with logitech mice... I have a Performance MX working fantastically on my linux box with KDE4 (kubuntu 10.10). Some interesting points:

 

1) All buttons are detected with last kernel... at least with

 

$ uname -a
Linux tuxica 2.6.35-22-generic #35-Ubuntu SMP Sat Oct 16 20:45:36 UTC 2010 x86_64 GNU/Linux

 

2) So, basically, you only need to map those buttons with desired actions. How to know with button is pressed and the correspondent numeric code? Well, you can use the 'xev' program:

 

$ xev

 

This program is a key and mouse events sniffer. When it's running, you can see a window in which you can press mouse buttons and see if they are detected. For example, with the zoom button of the Performance MX you will see something like that:

 

ButtonPress event, serial 35, synthetic NO, window 0x5800001,
    root 0x15a, subw 0x0, time 64521438, (84,117), rootSmiley Sad88,144),
    state 0x10, button 13, same_screen YES

 

that means that 13 is the code for that mouse button. You can try every mouse buttons on your hand Smiley Happy ... for easy access, here is the map for Performance MX:

 

Back button: 8

Forward button: 9

Zoom button: 13

Show windows button: 10

 

the other buttons are well recognized and you don't need to map to actions.

 

3) Now, you need to install a little program to re-map mouse and keyboard inputs. The magician is 'xbindkeys' ... the easy installation is using:

 

$ sudo apt-get install xbindkeys

 

4) Once installed, you can do the magic. The idea is configure the mouse buttons to send key combinations to activate other desktop functionalities (as the matter of fact, xbindkeys can be used for execute any other program when you press a mouse button). For example, the "show windows" button is ideal for KDE's Present All Windows feature (for mac users, something similar to Expose). In KDE you can do that with Ctrl+F10 keys combination. The point is create a xbindkeys' configuration file to do the job.

 

5) To create the configuration file, just run the following command:

 

$ xbindkeys --defaults > $HOME/.xbindkeysrc

 

6) And we need to edit the file to specify your button's mapping:

 

$ kate $HOME/.xbindkeysrc

 

'kate' is the KDE's default plain text editor. Of course, you can use your favorite editor.


7) We need to add our button-to-key configurations. For example, I have the following:

 

# Back
"xte 'keydown Alt_L' 'key Left' 'keyup Alt_L'"
  b:8

# Forward
"xte 'keydown Alt_L' 'key Right' 'keyup Alt_L'"
  b:9

# Present desktops
"xte 'keydown Control_L' 'key F8' 'keyup Control_L'"
  b:13

# Present windows
"xte 'keydown Control_L' 'key F10' 'keyup Control_L'"
  b:10

8) There was a new requirement. the 'xte' program, which basically simulates user key press combinations. Install it using:

 

$ sudo apt-get install xte

 

Now, if you run on a terminal something like:

 

$ xte 'keydown Control_L' 'key F10' 'keyup Control_L'

 

that means simulate a Ctrl+F10 keypress. The idea is using xbindkeys to say: "when I press 13th mouse button, send a Ctr+F10 keyboard press using xte program to generate that"

 

9) And finally, you need to configure 'xbindkeys' to run automatically on system startup. Just go to System settings / Startup and Shutdown / Autostart / Add program button and type '/usr/bin/xbindkeys' on the dialog.

 

10) Othe tips: KDE is a very customizable environment, and you have a lot of options to configure exactly what you want. For example, if you want to map the "Zoom button" (or other on a different mouse such as RevolutionMX) with 'next desktop' action:

 

# Next desktop
"qdbus org.kde.kwin /KWin org.kde.KWin.nextDesktop"
   b:13

 

(qdbus is a very powerful way to communicate with applications in KDE)

 

Of course, you can use this option with Gnome or any other desktop environment.

 

Hope this helps someone,

 

Hugo

 

EOF
