# OSINT

## Certificate Transparency & Subdomains

```
https://www.crt.sh/?q=inlanefreight.com
https://crt.name/v1/search?apex=inlanefreight.com
```

```
curl -s https://crt.sh/\?q\=inlanefreight.com\&output\=json | jq
curl -s https://crt.sh/\?q\=inlanefreight.com\&output\=json | jq . | grep name | cut -d":" -f2 | grep -v "CN=" | cut -d'"' -f2 | awk '{gsub(/\\n/,"\n");}1;' | sort -u
```

## Hosted servers & IP addresses

```
for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f1,4;done
```

## Shodan

```
for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f4 >> ip-addresses.txt;done
for i in $(cat ip-addresses.txt);do shodan host $i;done
```

## DNS records

```
dig any inlanefreight.com
```
