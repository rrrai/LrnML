# Install Anaconda from 
https://www.anaconda.com/distribution/

Installed current version for your platform and extract
chmod +x AnacondaFile.sh

## Configure Anaconda for all users
Create a user for Anaconda
adduser anaconda
mkdir /opt/anaconda

Execute the anaconda install script and choose /opt/anaconda as the folder. Once installed chage the ownership of 
chown -R anaconda:anaconda /opt/anaconda 
chmod -R go-w /opt/anaconda 
chmod -R go+rX /opt/anaconda

# Create common environment for all users
su anaconda
conda create -n wft-ml
source /opt/anaconda/bin/activate wft-ml

/opt/anaconda/bin/conda create -n my_env package1 package2

## Use pip to install non conda pacakges for everyone
su anaconda
/opt/anaconda/bin/pip install pysolr
