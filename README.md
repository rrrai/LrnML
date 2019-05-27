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



# Configure remote desktop XRDP with Gnome

$ sudo apt-get install ubuntu-gnome-desktop

$ sudo apt-get install -y xrdp 

$ sudo systemctl enable xrdp

sudo sed -e 's/^new_cursors=true/new_cursors=false/g' \
           -i /etc/xrdp/xrdp.ini

    cat <<EOF > ~/.xsessionrc
    export GNOME_SHELL_SESSION_MODE=ubuntu
    export XDG_CURRENT_DESKTOP=ubuntu:GNOME
    export XDG_DATA_DIRS=/usr/share/ubuntu:/usr/local/share:/usr/share:/var/lib/snapd/desktop
    export XDG_CONFIG_DIRS=/etc/xdg/user-dirs.conf:/etc/xdg

    

$ sudo nano /etc/xrdp/xrdp.ini
    encrypt_level=high

sudo sed -i 's/allowed_users=console/allowed_users=anybody/' /etc/X11/Xwrapper.config

$ sudo nano /etc/polkit-1/localauthority.conf.d/02-allow-colord.conf

add following

    polkit.addRule(function(action, subject) {
    if ((action.id == "org.freedesktop.color-manager.create-device" ||
    action.id == "org.freedesktop.color-manager.create-profile" ||
    action.id == "org.freedesktop.color-manager.delete-device" ||
    action.id == "org.freedesktop.color-manager.delete-profile" ||
    action.id == "org.freedesktop.color-manager.modify-device" ||
    action.id == "org.freedesktop.color-manager.modify-profile") &&
    subject.isInGroup("{group}")) {
    return polkit.Result.YES;
    }
    });

Do this with root account due to permission

$ sudo nano /etc/polkit-1/localauthority/50-local.d/color.pkla

    [Allow colord for all users]
    Identity=unix-user:*
    Action=org.freedesktop.color-manager.create-device;org.freedesktop.color-manager.create-profile;org.freedesktop.color-manager.delete-device;org.freedesktop.color-manager.delete-profile;org.freedesktop.color-manager.modify-device;org.freedesktop.color-manager.modify-profile
    ResultAny=yes
    ResultInactive=yes
    ResultActive=yes

$ sudo add-apt-repository universe

$ sudo apt install gnome-tweak-tool -y

$ gnome-tweaks -> and turn on Extensions, Ubuntu appindicators and Ubuntu dock 

$ sudo ufw allow 3389/tcp

$ sudo systemctl restart xrdp

$ sudo /etc/init.d/xrdp restart


# Basic coding, ML, and scientific applications install
sudo apt-get install vim csh flex gfortran libgfortran3 g++ \
                     cmake xorg-dev patch zlib1g-dev libbz2-dev \
                     libboost-all-dev openssh-server libcairo2 \
                     libcairo2-dev libeigen3-dev lsb-core \
                     lsb-base net-tools network-manager \
                     git-core git-gui git-doc xclip gdebi-core
                     
