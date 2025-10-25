
# ZFS

Manages RAID and expose it as partitions for linux.

[Oracle ZFS doc](https://docs.oracle.com/cd/E19253-01/819-5461/index.html)

```sh
# create a pool named "raid1" in mirror mode (=RAID1) on the 2 hdd sda/sdb
# pool is like a partition as far a linux is concerned
# partition is mounted at "/raid1" ; but -m /mount_path can be used to change the path
sudo zpool create raid1 mirror /dev/sda /dev/sdb

# get all pool status, with disk state/failures
sudo zpool status

# destroy the pool "raid1"
sudo zpool destroy raid1
```


# Samba

Allows file sharing with Windows/other Linux machines.

```sh
sudo mkdir /raid1/shared
sudo apt install samba
```

Edit config file run nano and add the following disk
```sh
sudo nano /etc/samba/smb.conf
```
```conf
# shared = name of the shared virtual drive
# accessible via \\192.168.1.100\shared
[shared]
   path = /raid1/shared
   browseable = yes
   read only = no
   guest ok = yes
```

```sh
sudo systemctl restart smbd
```
