
# Introduction

Some notes on getting proprietary Nvidia drivers setup on debian based linux
machines.

# Proprietary Nvidia Driver

This step requires use of the virtual terminal (tty) reached by pressing
`Ctrl-Alt-F1`.  If you get a blank screen when doing that, the default
resolution is probably not compatible with the video card.  Move through
the function keys until you get back to your X-window (i.e. `Ctrl-Alt-F2`,
`Ctrl-Alt-F3`, ...).  The default is usually `Ctrl-Alt-F6`.  Open a terminal
and Give the following commands,

    sudo sed -i -e 's/#GRUB_TERMINAL/GRUB_TERMINAL/g' /etc/default/grub
    sudo update-grub

Restart the computer to allow these changes to take effect. When it boots
back up, follow the steps below to install the driver.

  * Go to the
    [Nvidia Driver Download](http://www.nvidia.com/Download/index.aspx)
    and find the right driver.  Download the file to your machine
    (for example `NVIDIA-Linux-x86_64-346.59.run`).

  * Switch to the first tty (`Ctrl-Alt-F1`) and login.

  * Install the build-essential package
    (`sudo apt-get install build-essential`)

  * Stop the display manager (`sudo /etc/init.d/mdm stop`).  Note `mdm` is
    the default for Mint, might be `lightdm` or `gdm` for other flavors.

  * Run the install script (`sudo sh ./NVIDIA-Linux-x86_64-346.59.run`)

Reboot and you're good.
