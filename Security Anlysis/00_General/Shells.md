# <h1 style="text-align:center">Shells</h1>

## Shell Types

Once an vulnerability has been exploited, our next goal is to create a reliable connection that gives us access to the sytems shell (i.e. ```Bash``` or ```PowerShell```). One way to achieve this is by using tools such as ```SSH``` on Linux or ```WinRM``` on Windows. However, to do this, we need credentials.

Another method is through shells. There are three main types of shells: Reverse Shell, Bind Shell, and Web Shell.

### Reverse Shell
Most common, quickest, and easiest method. We can start a netcat listener on our machine that listens on a specific port. With listener in place, we can execute a ```reverse shell command``` that connects the remote system shell (e.g. ```Bash```, ```PowerShell```) to our netcat listener, giving us a reverse connection over the remote system. 

* ```nc -lvnp <port number>``` - start a netcat listener on a port of our choosing.
* 