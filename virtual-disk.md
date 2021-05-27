# How to do this do with `dd` 

1 - do `dd`
```
sudo dd if=/dev/zero of=vdisk0.img bs=100M count=100 iflag=fullblock status=progress
```
2 - after `dd` do : `mkfs`
```
sudo mkfs.ext4 -f vdisk0.img
```

3 - and `mount`
```
sudo mount vdisk0.img /mnt
```

## _Now you can reformat into XFS under an LUKS if you want...._  ;) 
