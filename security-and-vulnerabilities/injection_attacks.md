### SQL injection
> Inject SQL commands that are interpreted by the database such as unauthorized data retrieval, modification, deletion.
```sql
SELECT * FROM users WHERE username = 'admin' --' AND password = 'password';
```
### LDAP
Similar to SQL injection. Happens when the input is not sanitized.
```
(&(user=*)(password=*))
```
### XSS
Allows malicious user to inject client-side scripts (commonly JavaScript) that are interpreted by the victim's browser. It occurs when an application fails to properly sanitize user input, allowing attackers to inject scripts.
```javascript
<script>document.cookie = "stolen=" + document.cookie;</script>
```
### CRLF (Carriage Return Line Feed) 
Malicious user injects newline characters (`\r\n`) that are interpreted by the server, altering HTTP header or log files. 
```bash
GET / HTTP/1.1\r\n
Host: victim.com\r\n
X-Forwarded-For: 127.0.0.1\r\n
\r\n
# possibilityof spoofing IP addresses or inject malicious data
```
### XPath
Occurs when an application improperly processes user input within an XPath query. 
```
//user[username/text()='admin' or '1'='1' and password/text()='password']
```
### SMTP/IMAP
 Allows malicious user to inject SMTP commands or IMAP commands that are interpreted by the end SMTP/IMAP system.
 
Most common case is spamming.
### Code injection
Injected code that is interpreted by the application’s runtime environment. Occurs when an application directly executes user-provided input as code.
```javascript
// If an attacker sends ?code=phpinfo(), it will execute
eval($_GET['code']);
```
### OS command injection
Injected system commands that are interpreted by the operating system.
```bash
# If the input is directly passed to system() or exec() 
ping -c 4 example.com; rm -rf /
```
### Host header injection
Allows a malicious user to manipulate the `Host` header that is interpreted by the server. Happens when a server relies on the Host header without proper validation. 
```bash
# If an application generates password reset links using the `Host` header, an attacker can redirect victims to a malicious site.
GET / HTTP/1.1
Host: attacker.com
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1OTMyNjUxNjRdfQ==
-->