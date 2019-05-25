# Install Anaconda from 
https://www.anaconda.com/distribution/

Installed current version for your platform and extract
chmod +x Anaconda3-2019.03-Linux-x86_64.sh

## Configure Anaconda for all users
Create a user for Anaconda

sudo adduser anaconda

sudo ./Anaconda3-2019.03-Linux-x86_64.sh -b -p /opt/anaconda


### Execute the anaconda install script and choose /opt/anaconda as the folder. Once installed chage the ownership and execution previlages of installed directory

sudo chown -R anaconda:anaconda /opt/anaconda 

sudo chmod -R go-w /opt/anaconda 

sudo chmod -R go+rX /opt/anaconda

# Create common environment for all users

su anaconda

conda create -n wft-ml

source /opt/anaconda/bin/activate wft-ml

/opt/anaconda/bin/conda create -n my_env package1 package2

# Use pip to install non conda pacakges for everyone
su anaconda
/opt/anaconda/bin/pip install packageX
