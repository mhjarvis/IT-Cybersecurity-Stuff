<h1 style="text-align:center">File Inclusion</h1>

Web applications are sometimes written to request files, or, in the case of search engines, to query certain results.

For example, a `GET` request in a search engine looks like:

`https://www.google.com/search?q=GoldenRetrievers`

The same applies to files:

`http://webapp.com/get.php?file=userCV.pdf`

File inclusiong vulnerabilities happen because requests are often not sanitized or validated. In this case, the user can pass any input into the function. This leads to leaked data or even used to gain remote command execution (`RCE`).

## Path Traversal

Also known as `Directory traversal`, allows someone to read operating system resources (local files on a server). A web application's URL can be abused to locate files/directories stored outside the application's root directory.

`https://www.php.net/manual/en/function.file_get_contents.php` - php get file contents function.

Path traversal attacks are also known as `dot-dot-slash` attacks. The attacker may send something like `file=../../../../etc/passwd`. On Windows, it can get the boot.ini file with `../../../../boot.ini`.

OS files that could be used when testing:

- `/etc/issue` - contains message or system identification to be printed before the login prompt.
- `/etc/profile` - controls system-wide default variables, such as Export variables, File creation mask (umask), Terminal types, Mail messages to indicate when new mail has arrived.
- `/proc/version` - version of Linux kernel.
- `/etc/passwd` - registered user that access a system.
- `/etc/shadow` - contains information about the system's users' passwords.
- `/root/.bash_history` - history commands for root.
- `/var/log/dmessage` - global system messages, including the messages that are logged during system startup.
- `var/mail/root` - all emails for root user.
- `/root.ssh/id_rsa` - private SSH keys for a root or any known valid user on the server.
- `/var/log/apache2/access.log` - accessed requests for Apache webserver.
- `C:\boot.ini` - boot options for compputers with BIOS firmware.

## Local File Inclusion (LFI)

http://10.10.133.153/lab3.php?file=../../../../etc/passwd%00

....//....//....//....//etc/passwd.

../../../../etc/passwd.

THM-profile/../../../../etc/passwd

## Remote File Inclusion

Remote File Inclusion (RFI) is a technique to include remote files into a vulnerable application. Like LFI, the RFI occurs when improperly sanitizing user input, allowing an attacker to inject an external URL into include function. One requirement for RFI is that the allow_url_fopen option needs to be on.

## Remediation

Keep system and services, including web application frameworks, updated with the latest version.
Turn off PHP errors to avoid leaking the path of the application and other potentially revealing information.
A Web Application Firewall (WAF) is a good option to help mitigate web application attacks.
Disable some PHP features that cause file inclusion vulnerabilities if your web app doesn't need them, such as allow_url_fopen on and allow_url_include.
Carefully analyze the web application and allow only protocols and PHP wrappers that are in need.
Never trust user input, and make sure to implement proper input validation against file inclusion.
Implement whitelisting for file names and locations as well as blacklisting.
