#NVIDIA-Switch

This is a methord for switchable graphics on NVIDIA optimus notebooks in bash, that displays the X server directly on that device, by utalising the NVIDIA optimus solution, but the issue with that is the lack of ability to select the INTEL intergrated graphics easily. This set of bash scripts works to resolve that by implimenting a set of scripts to run at login that gives the user a simple prompt to select the card to be used. It has inbuilt options to edit the configs which can be used by relaunching the scripts whilst X is running

#CURRENT SUPPORT FOR
1. GENTOO
2. DEBIAN
3. UBUNTU
4. LINUX MINT
5. ELEMENTORY OS

###UPDATE 1
Other Distro Support

1. Elementory Os
2. Debian
3. Ubuntu
4. Linux Mint

###UPDATE 2
We now can run the script without sudo premissions, see bellow for instructions


Adding any other Ubuntu or debian based release is as easy as adding the lsb_release -si output into the nvidia-switch and intel-switch script
Special thanks for Debian/Ubuntu based distro from marquis196, whos use of update-alternatives for opengl selection in Debian/Ubuntu was the peice I was looking for to make it work on these systems
https://github.com/maquis196/optirun-prime-switcher


ALSO SINGLE USER ONLY, though if there is demand, per user profiles can be implimented
lastly there is the requirement to place the users password in to change graphics, but down the line this may change if it is implimented as a systemd service and the script calls through somthing like D-BUS

The script needs all forms of graphical login disabled, to go straight to console, as this needs to run before X

Requirements

1. sudo
2. bash
3. nvidia proprietary drivers --if theres demand i can release a nouveau version
4. intel xorg drivers
5. mesa
6. bbswitch kernel module
7. eselect-opengl ONLY FOR GENTOO
8. update-alternatives FOR DEBIAN BASED


To install, copy the contents of the GIT to a folder on the users computer, and edit the line in login-script.sh, nvidia-switch-startx and intel-switch-startx line: export INS_DIR="/home/christian/.nvidia-switch" and change the location to the installed location
to run on boot add an entry to /etc/profile.d/motd.sh which points to the login-script.sh
add an entry to /etc/sudoers as follows

```
christian ALL = (ALL) NOPASSWD: /home/christian/.nvidia-switch/intel-switch
christian ALL = (ALL) NOPASSWD: /home/christian/.nvidia-switch/nvidia-switch
```

When the script is exercuted the user will be greeted with this screen (but in color, taste the rainbow)

 ```
 Welcome to NVIDIA Optimus dual-gpu graphical selection menu
Please select a GPU to start the X session inside your xinitrc, or stay at terminal

 Nvidia Dedicated GPU (n)
 Intel intergrated graphics (i)
 Stay at tty (t)
 Advancd options (a)

GPU SELECTION (n/i/t/a)? 
```

Simply type the letter corosponding to the GPU to start it
Config may be required first so press a and click enter, and you get advanced options

```
Welcome to advanced options
Helper scripts available are as follows....

Edit NVIDIA xinitrc file (q)
Edit INTEL xinitrc file (w)
Edit NVIDIA xorg.conf (a)
Edit INTEL xorg.conf (s)
Turn Off NVIDIA Card (z)
Turn On NVIDIA Card (x)
NVIDIA card status (c)
Edit nvidia-switch script (n)
Edit intel-switch script (i)
Back to previous menu (b)

Advanced Option Selection (q/w/a/s/z/x/c/n/i/b)?
```

There is an example xinitrc preset and xorg.config, as per the arch wiki
https://wiki.archlinux.org/index.php/NVIDIA_Optimus
But may need to be edited for certain users, please use the tool provided to edit them to prevent errors due to wrong edited file

Users who use a window manager which can require a different config please edit option (n) and (i) in the menu to add them, an example is given of i3wm config
