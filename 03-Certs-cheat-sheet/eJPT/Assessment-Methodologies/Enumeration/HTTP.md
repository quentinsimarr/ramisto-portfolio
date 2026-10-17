# Nmap

```
nmap -sV --script=http-enum -p80 <target>
```

```
nmap -sV --script=http-headers -p80 <target>
```

```
nmap -sV --script=banner -p80 <target>
```

```
nmap -sV --script=http-headers --script-args http-methods.url-path=/webdav/ -p80 <target>
```

```
nmap -sV --script=http-webdav-scan --script-args http-methods.url-path=/webdav/ -p80 <target>
```

# Metasploit framework

```
msf6 > use auxiliary/scanner/http/http_version
```

```
msf6 > use auxiliary/scanner/http/brute_dirs
```

```
msf6 > use auxiliary/scanner/http/robots_txt
```

# HTTP fingerprint

```
http <target>
```

# Directory listing

```
dirb <target>
```

# Directories hidden from search engines

```
https://example.org/robots.txt  
https://example.org/sitemap.xml  
https://example.org/sitemaps.xml
```

# Web technologies being used

Firefox add-ons :

- [BuiltWith](https://addons.mozilla.org/en-US/firefox/addon/builtwith/)
- [Wappalyzer](https://addons.mozilla.org/en-US/firefox/addon/wappalyzer/)

# Web scanner

```
whatweb example.org
```

```
nikto example.org
```

```
nuclei example.org
```

# CLI Browser

```
lynx http://<target>
```