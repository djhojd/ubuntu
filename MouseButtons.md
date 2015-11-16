# Extra Mouse Buttons

http://askubuntu.com/a/246849/41705
http://blog.hanschen.org/2009/10/13/mouse-shortcuts-with-xbindkeys/

```bash
sudo apt-get install xbindkeys xev  
```

You need to find the button numbers for the buttons on your mouse. Run xev. You will see a litle white windows appear, put your mouse in it and press your mouse buttons.

```bash
xev -event mouse | grep Button --before-context=1 --after-context=2
or
xev | grep -A2 ButtonPress
```

Create the xbindkeys config file using:

```bash
xbindkeys --defaults > $HOME/.xbindkeysrc  
```

Next we need to add the key/button bindings to the config file. You can open this file with gedit $HOME/.xbindkeysrc. 
To make a button act as Ctrl we would add:
```
"xte 'key Control_L'"
b:1  
```
This would bind Ctrl to mouse button one.
