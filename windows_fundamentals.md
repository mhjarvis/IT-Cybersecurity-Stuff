# Windows OS Fundamentals

## File System

Modern versions of Windows use the `New Technology File System (NTFS)`. Before that, it was the `FAT16/FAT32 (File Accocation Table)` and `HPFS (Hight Performance File System)`. FAT partions are still used on USB devices or MicroSD cards.

NTFS is a journaling file system, meaning that it can automatically repair the folders/files on disk using information stored in a log file.
NTFS also allows you to set permissions that grand/deny access to files and folders. Permissions are:

- Full controls
- Modify
- Read & Execute
- List folder contents
- Read
- Write

NTFS also has `Alternate Data Streams (ADS)`. ADS allows files to have more than one stream of data.

## Windows\System32 Folders

This usually contains the Windows OS. System environment variable for the Windows directory is `%windir%`.

The System32 folder holds the important files that are critical for the operating system.

# User Management

`lusrmgr.msc` - access to Local User and Group Management

## Computer Management

`compmgmt` - utility that controls System Tools, Storage, and Services and Applications.

`resmon` - Resource monitor

## Command Prompt

`hostname` - computer name
`whoami` - logged in user
`ipconfig` - shows network address settings for the computer
`/?` - retrieve help manual for a command
`cls` - clear screen
`netstat` - displays protocol statistics and current TCP/IP network connections
`net` - used to manage network resources

`regedit` - windows register
