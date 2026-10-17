# SNMP

## Explanation

- SNMP (Simple Network Management Protocol) is a widely used protocol for monitoring and managing networked devices, such as routers, switches, printers, servers, and more.

- It allows network administrators to query devices for status information, configure certain settings, and receive alerts or traps when specific events occur.

- Versions of SNMP :
    - SNMPv1 : The earliest version, using community strings (essentially passwords) for authentication.
    - SNMPv2c : An improved version with support for bulk transfers but still relying on community strings for authentication.
    - SNMPv3 : Introduced security features, including encryption, message integrity, and user-based authentication.

- Ports :
    - Port 161 (UDP) : Used for SNMP queries.
    - Port 162 (UDP) : Used for SNMP traps (notifications).

# Nmap

```
nmap -sU -sV -p 161 <target>
nmap -sU -p 161 --script=snmp-brute <target>
nmap -sU -p 161 --script=snmp* <target> > snmp_info
```

# Snmpwalk

```
snmpwalk -v 1 -c public
```
