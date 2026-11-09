# MySQL

## Default Configuration

```
cat /etc/mysql/mysql.conf.d/mysqld.cnf | grep -v "#" | sed -r '/^\s*$/d'
```

## Dangerous Settings

```
user =	Sets which user the MySQL service will run as.
password =	Sets the password for the MySQL user.
admin_address =	The IP address on which to listen for TCP/IP connections on the administrative network interface.
debug =	This variable indicates the current debugging settings
sql_warnings =	This variable controls whether single-row INSERT statements produce an information string if warnings occur.
secure_file_priv =	This variable is used to limit the effect of data import and export operations.
```

## Footprinting the Service

```
sudo nmap 10.129.14.128 -sV -sC -p3306 --script mysql*
```

## Interaction with the MySQL Server

```
mysql -u root -h 10.129.14.132
mysql -u root -pP4SSw0rd -h 10.129.14.128
```

## SQL commands

```
show databases;	Show all databases.
use <database>;	Select one of the existing databases.
show tables;	Show all available tables in the selected database.
show columns from <table>;	Show all columns in the selected table.
select * from <table>;	Show everything in the desired table.
select * from <table> where <column> = "<string>";	Search for needed string in the desired table.
```

