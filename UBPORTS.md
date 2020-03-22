## rootfs is read-only
Remount the rootfs:
```
# mount -o rw,remount /
```

## USB Internet

Once you're booted to the rootfs, you can access the internet via USB by running these commands:

**On Phone/Tablet:**
```
# route add default gw 10.15.19.100
# echo nameserver 80.80.80.80 | sudo tee /etc/resolv.conf
```

**On host machine:**
```
# sysctl net.ipv4.ip_forward=1
# iptables -P FORWARD ACCEPT
# iptables -A POSTROUTING -t nat -j MASQUERADE -s 10.15.19.0/24
```
