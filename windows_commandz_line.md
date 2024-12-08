# Windows Command Line

## Basic System Information

`set` - show enviornment variables.

`ver` - show operating system version.

`systeminfo` - various information such as OS info, system details, processor, memory

`more` - used for piping; (e.g. `driverquery | more`).

`help` - provides help information for a command.

`cls` - clears command prompt.

## Network Configuration

`ipconfig` - check network information.

`ipconfig /all` - more information about your network.

`ping taret_name` - sends ICMP packet and listens for response.

`tracert target_name` - trace route the network uses to traverse to the target.

`nslookup` - looks up a host/domain and returns its IP address.

`netstat` - displays current network connections and listening ports.

`netstat -a` - displays all established connections and listening ports.

`netstat -b` - shows the program associated with each listening port and established connection.

`netstat -o` - reveals the process ID (PID) associated with the connection.

`netstat -n` - uses a numerical form for addresses and port numbers.

`netstat -abon` - combines all four.

## File and Disk Management

`cd` - alone will list current drive and directory.

`dir` - view child directories.

`dir /a` - display hidden and system files as well.

`dir /s` - displays files in the current dir and subdirectories.

`tree` - visually represent the child directories and subdirectories.

`cd target_directory` - change to target_directory.

`cd ..` - go up one level.

`mkdir directory_name` - make directory.

`rmdir directory_name` - remove directory.

`type` - see contents of a file.

`copy` - copy file (e.g. `copy test.txt test2.txt).

`move` - move files.

`del` or `erase` - remove file.

`*` - wildcard character; can be used to refer to multiple files.

## Task and Process Management

`tasklist` - list the running processes.

`tasklist /?` - help page.

`tasklist /FI "imagename eq notepad.exe"` - find running processes related to notepad.exe.

`taskkill /PID target_pid` - terminate any task.

## Conclusion

`chkdsk` - checks the file system and disk columes for errors and bad sectors.

`driverquery` - displays a list of installed devices.

`sfc /scannow` - scans system files for corruption and repairs them if possible.
