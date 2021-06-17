# How to do this do with `dd` 
creation of an virtual disk under linux

1 - do `dd`
```
sudo dd if=/dev/zero of=vdisk0.img bs=100M count=100 iflag=fullblock status=progress
```
2 - do `cfdisk`
```
sudo cfdisk vdisk0.img
```
and create the table of partition

3 - after `dd` do : `mkfs`
```
sudo mkfs.ext4 -f vdisk0.img
```

4 - and `mount`
```
sudo mount vdisk0.img /mnt
```

## _Now you can reformat into XFS under an LUKS if you want...._  ;) 


# Encrypted virtual disk (LUKS)
create the folder `vdisks` with `mkdir -p /vdisks`
1 - do `dd`
```
sudo dd if=/dev/random of=/vdisks/secret-data.img bs=100M count=100 iflag=fullblock status=progress
```

2 - after `dd` do `cfdisk`
```
sudo cfdisk /vdisks/secret-data.img
```
and create the table of partition

3 - after have do `cfdisk`please do `cryptsetup` to format
```
sudo cryptsetup luksFormat /vdisks/secret-data.img
```
set your password of this disk(asked)

4 - mount the disk with this
_an password can be asked_
```
sudo cryptsetup luksOpen /vdisks/secret-data.img secret
sudo mount /dev/mapper/secret /mnt
```

And if you want unmount
```
sudo umount /mnt && sudo cryptsetup luksClose /dev/mapper/secret
```

...Now you know how to do this 
