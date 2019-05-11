# Encrypt the new home partition

([Source](https://feeding.cloud.geek.nz/posts/encrypting-your-home-directory-using/))

Log into root:

```bash
sudo su
```

Encrypt the home partition.

```bash
umount /home
cryptsetup -h sha256 -c aes-xts-plain64 -s 512 luksFormat /dev/sda5
cryptsetup luksOpen /dev/sda5 chome
mkfs.ext4 -m 0 /dev/mapper/chome
```

Open the crypttab file:

```bash
nano /etc/crypttab
```

And add this line:

```conf
chome /dev/sda5 none luks,timeout=30
```

Open the fstab file:

```bash
nano /etc/fstab
```

And add this line:

```conf
/dev/mapper/chome /home ext4 nodev,nosuid,noatime 0 2
```

Reboot the system:

```bash
init 6
```
