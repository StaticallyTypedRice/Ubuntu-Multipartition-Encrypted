# Encrypt the new home partition

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



Reboot the system:

```bash
init 6
```
