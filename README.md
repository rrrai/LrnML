# LrnML
My machine learning Ubuntu Environment

# Update Ubuntu after install

sudo apt-get update
sudo apt-get upgrade

# Install Samba to make the remote machine discoverable
sudo apt install samba
Make a directory to share files between windows desktop
mkdir /home/<username>/sambashare/
sudo nano /etc/samba/smb.conf
and add following at the bottom
[sambashare]
    comment = Samba on Ubuntu
    path = /home/username/sambashare
    read only = no
    browsable = yes
sudo service smbd restart    

# Configure VNC with Gnome
sudo apt-get install ubuntu-desktop gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal -y
sudo apt-get -y install tightvncserver
vncserver
ps -ef | grep Xtightvnc
vncserver -kill :X 
cp ~/.vnc/xstartup ~/.vnc/xstartup_backup
nano ~/.vnc/xstartup

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



# Configure remote desktop with MATE
sudo apt-get install xrdp 
sudo systemctl enable xrdp
sudo apt-get install mate-core mate-desktop-environment mate-notification-daemon
sudo sed -i.bak '/fi/a #xrdp multiple users configuration \n mate-session \n' /etc/xrdp/startwm.sh
sudo ufw allow 3389/tcp
sudo /etc/init.d/xrdp restart

# Basic coding, ML, and scientific applications install
sudo apt-get install vim csh flex gfortran libgfortran3 g++ \
                     cmake xorg-dev patch zlib1g-dev libbz2-dev \
                     libboost-all-dev openssh-server libcairo2 \
                     libcairo2-dev libeigen3-dev lsb-core \
                     lsb-base net-tools network-manager \
                     git-core git-gui git-doc xclip gdebi-core
                     
