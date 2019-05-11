# Create a separate home partition

([Source](https://askubuntu.com/a/50539))

Use a partition tool to create an ext4 partition on your drive of choice.

Log into root:

```bash
sudo su
```

Go to the root home folder (or somewhere outside `/home`):

```bash
cd ~
```

Mount the partition:

```bash
mkdir /mnt/tmp
mount /dev/sdb1 /mnt/home
```

Where `sdb1` is your new partition. Change this as necessary, using `lsblk` to see the partitions.

Back up the home folder (preferably make a second backup to a removable drive or the cloud):

```bash
mkdir /homebackup
cp -a /home /homebackup
```

Mount the new partition to the location of the home partition:

```bash
mount /dev/sdb1 /home
```

Unmount and delete the existing home partition:

```bash
umount /home
rm -rf /home/*
```

Take note of the UUID of the new home partition using blkid:

```bash
blkid
```

Open the fstab file:

```bash
nano /etc/fstab
```

Paste the following line, changing the UUID to what blkid displayed:

```conf
UUID=(partition-uuid) /home ext4 defaults 0 2
```

**Do not reboot the system at this time, otherwise you will not be able to log in!**

**[Previous Step](./0%20-%20Initial%20setup.md)** || **[Next Step](./1%20-%20Encrypt%20home%20partition.md)**
