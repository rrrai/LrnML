# LrnML
Machine learning Ubuntu Environment Setup

# Update Ubuntu after install

$ sudo apt-get update

$ sudo apt-get upgrade



# Install Terminator terminal
$ sudo apt-get install terminator 

# Install Samba to make the remote machine discoverable
$ sudo apt install samba

Make a directory to share files between windows desktop

$ mkdir /home/<username>/sambashare/

add following at the bottom

$ sudo nano /etc/samba/smb.conf

    [sambashare]
    comment = Samba on Ubuntu
    path = /home/username/sambashare
    read only = no
    browsable = yes

$ sudo service smbd restart    



# Configure VNC with Gnome

sudo apt-get install ubuntu-desktop gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal -y

sudo apt-get -y install tightvncserver

test the server
$ vncserver

ps -ef | grep Xtightvnc
vncserver -kill :X 
cp ~/.vnc/xstartup ~/.vnc/xstartup_backup

nano ~/.vnc/xstartup

Edit the file to reflect following

    #!/bin/sh
    def
    export XKL_XMODMAP_DISABLE=1
    unset SESSION_MANAGER
    unset DBUS_SESSION_BUS_ADDRESS

xrdb $HOME/.Xresources
xsetroot -solid grey

gnome-session &
vncserver
vncserver -geometry 1920x1080 -depth 24



# Basic coding, ML, and scientific applications install
sudo apt-get install vim csh flex gfortran libgfortran3 g++ \
                     cmake xorg-dev patch zlib1g-dev libbz2-dev \
                     libboost-all-dev openssh-server libcairo2 \
                     libcairo2-dev libeigen3-dev lsb-core \
                     lsb-base net-tools network-manager \
                     git-core git-gui git-doc xclip gdebi-core
                     
