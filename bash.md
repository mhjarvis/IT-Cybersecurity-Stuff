# Linux Commands

## Filesystem Interaction

`ls` - listing

`ls -a` - show all (includes hidden files)

`cd` - change directory

`cat` - concatenate

`pwd` - print working directory

## Searching for Files

`find` - find / search

`find -name passwords.txt`

`find -name *.txt`

`grep` - search the contents of files for specific values.

`grep '81.144.123.80' access.log`

## Operators

`&` - allows you to run commands in the background of your terminal.

`&&` - allows you to combine multiple commands together in one line of your terminal.

`>` - redirector - take the output from a command and direct it elsewhere.

`>>` - same as `>` but appends the output rather than replacing it.

## Filesystem Interaction

`touch` - create file

`mkdir` - create a folder

`cp` - copy a file/folder

`mv` - move file or folder

`rm` - remove file or folder; use `-R` if removing directory

`file` - determine the type of a file

## Permissions

`ls -lh` - show permissions (-h human readable)

`su` - switch between users

`su user2` - use su to switch to user2

`su -l user2` -

## Downloading / Transfering Files

`wget` - allows you to download files via HTTP.

`wget https://assets.tryhackme.com/additional/linux-fundamentals/part3/myfile.txt`

`SCP` - allows you to transfer files between two computers using SSH.

`scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt` - transfer file to the other system

`scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt` -transfer file from a system to yours.
