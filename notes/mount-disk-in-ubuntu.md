- find new disk
```shell
lsblk
```

- check disk partition
```shell
fdisk -l /dev/xvdf
```

- disk partition
```shell
sudo fdisk /dev/xvdf
```
```file
a   toggle a bootable flag
b   edit bsd disklabel
c   toggle the dos compatibility flag
d   delete a partition
l   list known partition types
m   print this menu
n   add a new partition
o   create a new empty DOS partition table
p   print the partition table
q   quit without saving changes
s   create a new empty Sun disklabel
t   change a partition’s system id
u   change display/entry units
v   verify the partition table
w   write table to disk and exit
x   extra functionality (experts only)
```
```file
n
p
1


w
```

- format disk
```shell
sudo mkfs.ext4 /dev/xvdf1
```

- find disk uuid
```shell
ls -al /dev/disk/by-uuid/
```

- mount disk
```shell
vi /etc/fstab
```
```file
UUID=e942647c-788f-405e-a9a2-9a46887805d8 /mount/path ext4 noatime,nodiratime,discard,defaults 0 1
```
```shell
mount /mount/path
```
