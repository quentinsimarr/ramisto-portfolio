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

