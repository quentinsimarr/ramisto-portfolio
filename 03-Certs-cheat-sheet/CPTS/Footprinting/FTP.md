# FTP

## Default configuration

```
cat /etc/vsftpd.conf | grep -v "#"
cat /etc/ftpusers
```

## Dangerous settings

```
anonymous_enable=YES	: Allowing anonymous login?
anon_upload_enable=YES	: Allowing anonymous to upload files?
anon_mkdir_write_enable=YES	: Allowing anonymous to create new directories?
no_anon_password=YES	: Do not ask anonymous for password?
anon_root=/home/username/ftp	: Directory for anonymous.
write_enable=YES	: Allow the usage of FTP commands STOR, DELE, RNFR, RNTO, MKD, RMD, APPE, and SITE?
```

## Anonymous login

```
ftp 10.129.14.136
```

### vsFTPd commands

```
ftp> status
ftp> debug
ftp> trace
ftp> ls
ftp> ls -R
ftp> get Important\ Notes.txt
```

## Download all available files

```
wget -m --no-passive ftp://anonymous:anonymous@10.129.14.136
```

## Upload files

```
On kali -> touch testupload.txt
On FTP server -> put testupload.txt 
