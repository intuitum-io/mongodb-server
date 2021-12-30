# MongoDB Installation

This repository installs MongoDB 5.0 Community Edition on 20.04 LTS ("Focal". To install a different version of MongoDB Community Edition, visit the MongoDB Documentation.

## Pre-requisits

1. Unix OS (Host)
2. Vagrant >= 2.2.18
3. Virtualbox >= 6.1.2

## Build the Ubuntu Server using Vagrant

```sh
git clone https://github.com/intuitum-io/mongodb-server.git
```
cd mongodb-server

```sh
vagrant up 
```

```sh
vagrant ssh
```

## Import the public key used by the package management system.

From a terminal, issue the following command to import the MongoDB public GPG Key from https://www.mongodb.org/static/pgp/server-5.0.asc:

```sh
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -

sudo apt install gnupg

wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
```

## Create a list file for MongoDB.

Create the list file /etc/apt/sources.list.d/mongodb-org-5.0.list for your version of Ubuntu.

```sh
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list
```

## Reload local package database.

Issue the following command to reload the local package database:

```sh 
sudo apt update
```

## Install the MongoDB packages.

You can install either the latest stable version of MongoDB or a specific version of MongoDB.

```sh 
sudo apt-get install -y mongodb-org
```

## Run MongoDB Community Edition

To run and manage your mongod process, you will be using your operating system's built-in init system. Recent versions of Linux tend to use systemd (which uses the systemctl command), while older versions of Linux tend to use System V init (which uses the service command).

If you are unsure which init system your platform uses, run the following command:

```sh 
ps --no-headers -o comm 1
```
## Start MongoDB.

You can start the mongod process by issuing the following command:

```sh
sudo systemctl start mongod
```
Verify that MongoDB has started successfully.

```sh
sudo systemctl status mongod
```

Start MongoDB on boot.

```sh
sudo systemctl enable mongod
```

## Stop MongoDB.

As needed, you can stop the mongod process by issuing the following command:

```sh
sudo systemctl restart mongod
```
## Begin using MongoDB.

Start a mongosh session on the same host machine as the mongod. You can run mongosh without any command-line options to connect to a mongod that is running on your localhost with default port 27017.

```sh
mongosh
```

## Uninstall MongoDB Community Edition

To completely remove MongoDB from a system, you must remove the MongoDB applications themselves, the configuration files, and any directories containing data and logs. The following section guides you through the necessary steps.

**WARNING**

This process will completely remove MongoDB, its configuration and all databases. This process is not reversible, so ensure that all of your configuration and data is backed up before proceeding.

## Stop MongoDB.

Stop the mongod process by issuing the following command:

```sh
sudo service mongod stop
```
## Remove Packages.

Remove any MongoDB packages that you had previously installed.

```sh
sudo apt-get purge mongodb-org*
```

## Remove Data Directories.

Remove MongoDB databases and log files.

```sh
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongodb
```
