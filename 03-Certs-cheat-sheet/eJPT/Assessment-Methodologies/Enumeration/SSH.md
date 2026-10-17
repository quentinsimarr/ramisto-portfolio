# Nmap

```
nmap --script=ssh2-enum-algos -p 22 <target>
```

```
nmap --script=ssh-hostkey --script-args ssh_hotkey=full -p 22 <target>
```

```
nmap --script=ssh-auth-methods --script-args="ssh.user=admin" -p 22 <target>
```

# Netcat

```
nc -v <target> 22
```