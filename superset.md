# Apache Superset Installation in Debain
In this chapter I am describing the steps whcih I did for the installation of superset in my system. First of all let me tell that, for the easy installation of this visualization tool you have to install Python version 3.6 and virtual enviornment in your system.
Let's move directly to the steps:
For Debian and Ubuntu, the following command will ensure that the required dependencies are installed:
```
sudo apt-get install build-essential libssl-dev libffi-dev python-dev python-pip libsasl2-dev libldap2-dev
```
Ubuntu 16.04 If you have python3.5 installed alongside with python2.7, as is default on Ubuntu 16.04 LTS, run this command also:
```
sudo apt-get install build-essential libssl-dev libffi-dev python3.5-dev python-pip libsasl2-dev libldap2-dev
```
otherwise build for `cryptography` fails.

##Python virtualenv

It is recommended to install Superset inside a virtualenv. Python 3 already ships virtualenv, for Python 2 you need to install it. If it’s packaged for your operating systems install it from there otherwise you can install from pip:
```
pip install virtualenv
```
You can create and activate a virtualenv by:
```
# virtualenv is shipped in Python 3 as pyvenv
virtualenv venv
. ./venv/bin/activate
```
Once you activated your virtualenv everything you are doing is confined inside the virtualenv. To exit a virtualenv just type `deactivate`.
##Python’s setup tools and pip
Put all the chances on your side by getting the very latest `pip` and `setuptools`
```
pip install --upgrade setuptools pip
```

#Superset installation and initialization

Follow these few simple steps to install Superset.:
```
# Install superset
pip install superset

# Create an admin user (you will be prompted to set a username, first and last name before setting a password)
fabmanager create-admin --app superset

# Initialize the database
superset db upgrade

# Load some data to play with
superset load_examples

# Create default roles and permissions
superset init

# To start a development web server on port 8088, use -p to bind to another port
superset runserver -d
```
After installation, you should be able to point your browser to the right hostname:port `http://localhost:8088`, login using the credential you entered while creating the admin account, and navigate to Menu -> Admin -> Refresh Metadata. This action should bring in all of your datasources for Superset to be aware of, and they should show up in Menu -> Datasources, from where you can start playing with your data!

