# Encrypt the new home partition

([Source](https://feeding.cloud.geek.nz/posts/encrypting-your-home-directory-using/))

Log into root:

```bash
sudo su
```

We will assume that `sdb1` is your home partition. Change this as necessary, using `lsblk` to see the partitions.

Encrypt the home partition.

```bash
umount /home
cryptsetup -h sha256 -c aes-xts-plain64 -s 512 luksFormat /dev/sdb1
cryptsetup luksOpen /dev/sdb1 chome
mkfs.ext4 -m 0 /dev/mapper/chome
```

Open the crypttab file:

```bash
nano /etc/crypttab
```

And add this line:

```conf
chome /dev/sdb1 none luks,timeout=30
```

Open the fstab file:

```bash
nano /etc/fstab
```

And add this line:

```conf
/dev/mapper/chome /home ext4 nodev,nosuid,noatime 0 2
```

Restore the backed up home data:

```bash
mount /home
cp -a /homebackup/* /home
rm -rf /homebackup
```

Reboot the system:

```bash
init 6
```
