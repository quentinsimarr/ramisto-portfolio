# Nmap

First, find open ports quickly :

```
nmap -Pn -sS -p- -T4 <target>
```

```
nmap -Pn -sU -p- -T4 <target>
```

Get more information on running services and operating system :

```
nmap -Pn -sS -sV -O -p445 -T4 <target>
```

And increased aggressiveness of service version detection :

```
nmap -Pn -sS -sA --version-intensity 8 -p445 -T4 <target>
```

# Nmap scripting engine (NSE)

List all scripts :

```
ls -al /sur/share/nmap/scripts/
```

```
ls -al /sur/share/nmap/scripts/ | grep banner
```

Display help to specific script :

```
nmap --script-help=banner
```

Execute scripts :

```
nmap -sV --script=banner <target>
```

# Nmap Ouput Formats

Normal format :

```
nmap -oN output.txt
```

XML format :

```
nmap-oX output.xml
```

GREP format :

```
nmap -oG output.txt
```

# Import nmap XML file in Metasploit Framework

```
service postgresql start
```

```
msfconsole
msf6 > workspace -a pentest-1
msf6 > db_import output.xml
msf6 > hosts
msf6 > services
```

# Use Nmap in Metasploit Framework

```
msf6 > db_nmap -Pn -sS -A <target>
msf6 > hosts
msf6 > services
```