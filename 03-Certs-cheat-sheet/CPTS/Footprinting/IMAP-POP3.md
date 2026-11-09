# IMAP / POP3

## Default Configuration

https://doc.dovecot.org/2.4.1/core/summaries/settings.html

https://doc.dovecot.org/2.4.1/core/config/service.html

## IMAP Commands

```
1 LOGIN username password	User's login.
1 LIST "" *	Lists all directories.
1 CREATE "INBOX"	Creates a mailbox with a specified name.
1 DELETE "INBOX"	Deletes a mailbox.
1 RENAME "ToRead" "Important"	Renames a mailbox.
1 LSUB "" *	Returns a subset of names from the set of names that the User has declared as being active or subscribed.
1 SELECT INBOX	Selects a mailbox so that messages in the mailbox can be accessed.
1 UNSELECT INBOX	Exits the selected mailbox.
1 FETCH <ID> all	Retrieves data associated with a message in the mailbox.
1 CLOSE	Removes all messages with the Deleted flag set.
1 LOGOUT	Closes the connection with the IMAP server.
```

## POP3 Commands

```
USER username	Identifies the user.
PASS password	Authentication of the user using its password.
STAT	Requests the number of saved emails from the server.
LIST	Requests from the server the number and size of all emails.
RETR id	Requests the server to deliver the requested email by ID.
DELE id	Requests the server to delete the requested email by ID.
CAPA	Requests the server to display the server capabilities.
RSET	Requests the server to reset the transmitted information.
QUIT	Closes the connection with the POP3 server.
```

## Dangerous Settings

```
auth_debug	Enables all authentication debug logging.
auth_debug_passwords	This setting adjusts log verbosity, the submitted passwords, and the scheme gets logged.
auth_verbose	Logs unsuccessful authentication attempts and their reasons.
auth_verbose_passwords	Passwords used for authentication are logged and can also be truncated.
auth_anonymous_username	This specifies the username to be used when logging in with the ANONYMOUS SASL mechanism.
```
## Footprinting the Service

### NMAP

```
sudo nmap 10.129.14.128 -sV -p110,143,993,995 -sC
```

### CURL

```
curl -k 'imaps://10.129.14.128' --user user:p4ssw0rd
curl -k 'imaps://10.129.14.128' --user cry0l1t3:1234 -v
```

### OpenSSL - TLS Encrypted Interaction POP3 & IMAP

```
openssl s_client -connect 10.129.14.128:pop3s
openssl s_client -connect 10.129.14.128:imaps
```

