# SMB

## Default configuration

```
cat /etc/samba/smb.conf | grep -v "#\|\;"
```

## Dangerous settings

```
browseable = yes	Allow listing available shares in the current share?
read only = no	Forbid the creation and modification of files?
writable = yes	Allow users to create and modify files?
guest ok = yes	Allow connecting to the service without using a password?
enable privileges = yes	Honor privileges assigned to specific SID?
create mask = 0777	What permissions must be assigned to the newly created files?
directory mask = 0777	What permissions must be assigned to the newly created directories?
logon script = script.sh	What script needs to be executed on the user's login?
magic script = script.sh	Which script should be executed when the script gets closed?
magic output = script.out	Where the output of the magic script needs to be stored?
```

## Smbclient - List shares

```
smbclient -N -L //10.129.14.128
```

## Smbclient - Connect to share

```
smbclient //10.129.14.128/notes
```

## SMB commands

```
smb: \> help
smb: \> ls
smb: \> get prep-prod.txt
smb: \> !ls
smb: \> !cat prep-prod.txt
```

## Footprinting the service

```
sudo nmap 10.129.14.128 -sV -sC -p139,445
```
