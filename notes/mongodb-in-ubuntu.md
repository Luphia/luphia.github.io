## Setup SWAP
Check the System for Swap and Memory Information
```shell
sudo swapon -s
free -m
```
Check Available Space on the Hard Drive Partition
```shell
df -h
```
```file
/dev/vda1        20G  8.9G  9.8G  48% /
none            4.0K     0  4.0K   0% /sys/fs/cgroup
udev            235M  4.0K  235M   1% /dev
tmpfs            50M  336K   49M   1% /run
none            5.0M     0  5.0M   0% /run/lock
none            246M     0  246M   0% /run/shm
none            100M     0  100M   0% /run/user
```
Create a Swap File
```shell
sudo fallocate -l 4G /swapfile
```
Enabling the Swap File
```shell
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

## Install MongoDB
### UBUNTU
https://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/
```shell
### Import the public key used by the package management system ###
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927

### Create a list file for MongoDB ###
echo "deb http://repo.mongodb.org/apt/debian wheezy/mongodb-org/3.2 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list

### Reload local package database ###
sudo apt-get update

### Install the latest stable version of MongoDB ###
sudo apt-get install -y mongodb-org
```
## Configure
```shell
vi /etc/mongod.conf
```
```file
### Change listen port and allow remote connection ###
net:
  port: 2266
  bindIp: [127.0.0.1, remote_ip]

security:
  authorization: enabled
```

## Start mongodb with config file (background)
```shell
sudo mongod --config /etc/mongod.conf &
```

## Connect mongodb with client
```shell
mongo 127.0.0.1:27017

### close db
use admin
db.shutdownServer()
```

## Create Administrator for mongodb
```shell
use admin
db.createUser(
  {
    user: "admin",
    pwd: "password",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)
```

## Create Administrator for a single database
```shell
use singledb
db.createUser(
  {
    user: "singledbUserAdmin",
    pwd: "password",
    roles: [ { role: "userAdmin", db: "singledb" } ]
  }
)
```

## Add a User to a Database
```shell
use reporting
db.createUser(
    {
      user: "reportsUser",
      pwd: "12345678",
      roles: [
         { role: "read", db: "reporting" },
         { role: "read", db: "products" },
         { role: "read", db: "sales" },
         { role: "readWrite", db: "accounts" }
      ]
    }
)
```

## Connect mongodb with Authorization
```shell
mongo 127.0.0.1:27012/{$dbname} -u {$dbuser} -p {$dbpassword}
```

## Dump and Restore
```shell
# data lock
mongo 127.0.0.1:27012/admin -u {$dbuser} -p {$dbpassword}
db.runCommand({fsync:1,lock:1})
db.currentOp()

# dump
mongodump --host {$dbhost} --port 27012 --username {$dbuser} --password "{$dbpassword}" --out /dump/folder/

# data unlock
db.fsyncUnlock()

# restore
mongorestore -d {$dbname} --drop /dump/folder/ 
```
