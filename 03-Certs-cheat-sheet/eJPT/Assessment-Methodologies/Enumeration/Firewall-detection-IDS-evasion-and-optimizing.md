# Options

\-f : The -f option causes the requested scan (including host discovery scans) to use tiny fragmented IP packets. The idea is to split up the TCP header over several packets to make it harder for packet filters, intrusion detection systems, and other annoyances to detect what you are doing.

\-D : Causes a decoy scan to be performed, which makes it appear to the remote host that the host(s) you specify as decoys are scanning the target network too.

\-g : Simply provide a port number and Nmap will send packets from that port where possible.

\--host-timeout : Specify --host-timeout with the maximum amount of time you are willing to wait.

\--scan-delay : This option causes Nmap to wait at least the given amount of time between each probe it sends to a given host.

<h1>Firewall detect</h1>

ACK packets for detect filtered or unfiltered ports :  

```
nmap -sA -p80,445,3389 <target>
```

# IDS Evasion

Zombie scan :

```
nmap -Pn -sI <zombie-ip> <target> -v
```

Fragment packets :

```
nmap -f -p- <target>
```

Decoy scan with other IPs :

```
nmap -D <decoy-ip> -p- <target>
```

Source port scan :

```
nmap -g <source-port> -p- <target>
```

Sneaky mode :

```
nmap -T1 <target>
```

Paranoid mode :

```
nmap -T0 <target>
```

# Optimizing nmap

Specify 30m to ensure that Nmap doesn't waste more than half an hour on a single host :  

```
nmap --host-timeout 30m <target>
```

A ``--scan-delay`` of 1s will keep Nmap at that slow rate :

```
nmap --scan-delay 1s <target>
```