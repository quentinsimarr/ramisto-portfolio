# Nmap

```
nmap -sV --script=rdp-enum-encryption -p 3389 <target>
nmap -sV --script=rdp-ntlm-info -p 3389 <target>
nmap -sV --script=rdp-vuln-ms12-020 -p 3389 <target>
```

# Metasploit framework

```
service postgresql start && msfconsole
msf6 > search rdp_scanner
msf6 > use auxiliary/scanner/rdp/rdp_scanner
msf6 > set RHOSTS <target>
msf6 > set RPORT <port>
msf6 > run
```

## CVE-2019-0708 (BlueKeep)

```
msfconsole
msf6 > use auxiliary/scanner/rdp/cve_2019_0708_bluekeep
msf6 > set RHOSTS <target>
msf6 > run
```