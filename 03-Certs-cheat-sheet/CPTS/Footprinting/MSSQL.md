# MSSQL

## MSSQL Clients

https://learn.microsoft.com/en-us/sql/tools/sqlcmd/sqlcmd-utility?view=sql-server-ver15

https://docs.microsoft.com/en-us/sql/powershell/sql-server-powershell?view=sql-server-ver15

https://www.heidisql.com/

https://www.macsqlclient.com/

https://github.com/SecureAuthCorp/impacket/blob/master/examples/mssqlclient.py

```
locate mssqlclient

/usr/bin/impacket-mssqlclient
/usr/share/doc/python3-impacket/examples/mssqlclient.py
```

## MSSQL Databases

```
master =	Tracks all system information for an SQL server instance
model =	Template database that acts as a structure for every new database created. Any setting changed in the model database will be reflected in any new database created after changes to the model database
msdb =	The SQL Server Agent uses this database to schedule jobs & alerts
tempdb =	Stores temporary objects
resource =	Read-only database containing system objects included with SQL server
```

## Default Configuration

```
When an admin initially installs and configures MSSQL to be network accessible, the SQL service will likely run as NT SERVICE\MSSQLSERVER. Connecting from the client-side is possible through Windows Authentication, and by default, encryption is not enforced when attempting to connect.
```

## Dangerours Settings

```
- MSSQL clients not using encryption to connect to the MSSQL server
- The use of self-signed certificates when encryption is being used. It is possible to spoof self-signed certificates
- The use of named pipes
- Weak & default sa credentials. Admins may forget to disable this account
```

## Footprinting the Service

### NMAP

```
sudo nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 10.129.201.248
```

### MSSQL Ping in Metasploit

```
msf > use auxiliary/scanner/mssql/mssql_ping
```
### Connecting with Mssqlclient.py

```
python3 mssqlclient.py Administrator@10.129.201.248 -windows-auth
```
