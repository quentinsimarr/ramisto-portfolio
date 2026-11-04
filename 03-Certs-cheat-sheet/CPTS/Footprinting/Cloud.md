# Cloud 

## Hosted servers

```
for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f1,4;done
```

## Google Dorks

```
Amazon
intext:inlanefreight inurl:*amazonaws.com*

Azure
intext:inlanefreight inurl:blob.core.windows.net
intext:inlanefreight inurl:table.core.windows.net
intext:inlanefreight inurl:queue.core.windows.net
intext:inlanefreight inurl:file.core.windows.net
intext:inlanefreight inurl:database.core.windows.net
```
