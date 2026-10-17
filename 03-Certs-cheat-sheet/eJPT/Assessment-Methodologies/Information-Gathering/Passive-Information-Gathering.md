# DNS

```
host example.org
```

```
whois example.org
```

- [Dnsdumpster](https://dnsdumpster.com/)

- [Netcraft](https://sitereport.netcraft.com/)

# Source code

Use website vacuum cleaner to read source code without interacting with the target : [HTTrack](https://www.httrack.com/page/2/fr/index.html)

```
sudo apt install webhttrack
```

# Google Dorks

Limit to particular domain and subdomain :  

```
site:example.org
```

```
site:*.example.org
```

Limit particular word in url :  

```
inurl:admin
```

```
inurl:auth_user_file.txt
```

```
inurl:passwd.txt
```

```
inurl:login
```

Limit particular word in title :  

```
intitle:index of
```

Limit particular type of file :  

```
filetype:xlsx
```

# Search Engines

```
theHarvester -d example.org -b google,linkedin
```

Look a next version of website [Wayback Machine](https://archive.org)

Look [Have i been pwned?](https://haveibeenpwned.com/)