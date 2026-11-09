# SNMP

## Default Configuration

```
cat /etc/snmp/snmpd.conf | grep -v "#" | sed -r '/^\s*$/d'
```

## Dangerous Settings

```
rwuser noauth =	Provides access to the full OID tree without authentication.
rwcommunity <community string> <IPv4 address> = 	Provides access to the full OID tree regardless of where the requests were sent from.
rwcommunity6 <community string> <IPv6 address> = 	Same access as with rwcommunity with the difference of using IPv6.
```

## Footprinting the Service

### SNMPwalk

```
snmpwalk -v2c -c public 10.129.14.128
```

### OneSixtyOne

```
Ramisto@htb[/htb]$ sudo apt install onesixtyone
Ramisto@htb[/htb]$ onesixtyone -c /opt/useful/seclists/Discovery/SNMP/snmp.txt 10.129.14.128
```

### Braa

```
Ramisto@htb[/htb]$ sudo apt install braa
Ramisto@htb[/htb]$ braa <community string>@<IP>:.1.3.6.*   # Syntax
Ramisto@htb[/htb]$ braa public@10.129.14.128:.1.3.6.*
```
