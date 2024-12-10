# Bash (Bourne Again Shell)

## Types of Shells

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

## Processes

`ps` - view current processes

`ps aux` - view processes run by other users and those that don't run from a session (i.e. system processes)

`top` - shows real-time statistics about th eproccesses running on your system instead of a one-time view. Will refresh.

`kill` - terminate a process along with the PID number

    SIGTERM - kill the process, but allow it to do some cleanup
    SIGKILL - kill the process, does do any cleanup
    SIGSTOP - Stop/suspend a process

`Ctrl + Z` will background a process.

`fg` bring process to forground

## Cron and Crontabs

`crontab -e` - edit crontab

- - - - - command_to_execute

---

| | | | |
| | | | +---- Day of the week (0 - 7) [0 and 7 both represent Sunday]
| | | +------ Month (1 - 12)
| | +-------- Day of the month (1 - 31)
| +---------- Hour (0 - 23)
+------------ Minute (0 - 59)

example:

30 2 \* \* 1 /path/to/script.sh

## Other Commands

`echo $SHELL` - see which shell you are using.

`cat /etc/shells` - see which shells are available to you.
