# ICMP

```
ping <target>
```

```
fping -a -g <target> 2>/dev/null
```

# ARP

```
netdiscover -i eth0 -r <target>
```

# Nmap (ping scan)

```
nmap -sn <target>
```

```
nmap -sn <target> --send-ip
```

```
nmap -sn -iL targets.txt
```