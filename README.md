
# Introduction

A collection of notes on setting up debian based linux machines.  You'll need 
to install `git` before doing anything, 

    sudo apt-get install git

# Proprietary Nvidia Driver

This step requires use of the virtual terminal (tty) reached by pressing 
`Ctrl-Alt-F1`.  If you get a blank screen when doing that, the default 
resolution is probably not compatible with the video card.  Give the following 
commands,

    sudo sed -i -e 's/#GRUB_TERMINAL/GRUB_TERMINAL/g' /etc/default/grub
    sudo update-grub

  * Go to the 
    [Nvidia Driver Download](http://www.nvidia.com/Download/index.aspx)
    and find the right driver.  Download the file to your machine 
    (for example `NVIDIA-Linux-x86_64-346.59.run`).

  * Switch to the first tty (`Ctrl-Alt-F1`) and login.

  * Install the build-essential package 
    (`sudo apt-get install build-essential`)

  * Stop the display manager (`sudo /etc/init.d/mdm stop`).  
    Note `mdm` is the default for Mint, might be `lightdm` or `gdm` for other 
    flavors. 

  * Run the install script (`sudo sh ./NVIDIA-Linux-x86_64-346.59.run`)

Reboot and you're good. 


# Development Packages

Install some development packages system wide. 

    sudo apt-get install -y emacs texlive imagemagick
    sudo apt-get install -y zlib1g-dev libbz2-dev libssl-dev libreadline-dev
    sudo apt-get intsall -y gfortran
    sudo apt-get install -y libblas-dev liblapack-dev libatlas-dev
    sudo apt-get install -y libpng-dev dvipng libfreetype6-dev