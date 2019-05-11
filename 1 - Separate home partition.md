# Create a separate home partition

Use a partition tool to create an ext4 partition on your drive of choice

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

Copy the existing home folder to the new partition:

```bash
cp -a /home /mnt/home
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

Create user folders for the existing users on your system:
```bash
mkdir /home/user
```

Reboot the system:

```bash
init 6
```

**[Previous Step](./0%20-%20Initial%20setup.md)** || **[Next Step]()**
