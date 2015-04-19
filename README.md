
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

Restart the computer to allow these changes to take effect. When it boots 
back up, follow the steps below to install the driver. 

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

Install some development packages system wide.  You can copy/paste the 
commands below or run the scipt `install_dev_packages.sh` that is part 
of this git repo. 

    sudo apt-get install -y build-essential
    sudo apt-get install -y emacs24 texlive imagemagick gfortran libsqlite3-dev
    sudo apt-get install -y zlib1g-dev libbz2-dev libssl-dev libreadline-dev
    sudo apt-get install -y libblas-dev liblapack-dev libatlas-dev
    sudo apt-get install -y libpng-dev dvipng libfreetype6-dev
    sudo apt-get install -y qt4-dev-tools libqt4-dev

# Pyenv

Install this super cool software that allows you to run multiple versions
of python at once in a sensible way. Follow the instructions below or run
the script `install_pyenv.sh` (customize `.bashrc` to something else if you 
like). 

    git clone https://github.com/yyuu/pyenv.git ~/.pyenv

    echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
    echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
    echo 'eval "$(pyenv init -)"' >> ~/.bashrc
    exec $SHELL

Now run the command to install a few versions of python, 

    pyenv install 2.7.9
    pyenv rehash

    pyenv install 3.3.6
    pyenv rehash

    pyenv global 2.7.9
    

# PyQt4

This is a requirement of the interactive `Qt4Agg` backend for matplotlib.  You 
will have to run these commands once for each version of python you want to 
install matplotlib under. 

[sip download page](http://www.riverbankcomputing.com/software/sip/download)
get latest (e.g. `sip-4.16.7.tar.gz`) file and uncompress

    python configure.py 
    make install

[pyqt4 download page](http://www.riverbankcomputing.com/software/pyqt/download)
get latest (e.g. `PyQt-x11-gpl-4.11.3.tar.gz`) file and uncompress

    python configure-ng.py
    make install
