# <h1 style="text-align:center">Linux Fundamentals</h1>

## Linux Structure

Linux follows five core principles:

1. Everything is a file - all configuration files for various services that make Linux run are stored in text files. 
2. Small, single-purpose programs - numerous tools that work well together.
3. Ability to chain programs together to perform complex tasks - integration of different tools allow us to carry out complex tasks.
4. Avoid captive user interfaces - Linux is designed to work with the shell which provides increased control of the OS.
5. Configuration data stored in a text file - e.g. ```/etc/passwd``` stores all users on the system.

Linux components consist of:

1. Bootloader - code that guides the boot process (e.g. GRUB).
2. Kernel - main component of the OS; manages resources for the systems I/O devices at hardware level.
3. Daemons - background services; make sure key functions are working correctly; load after boot. 
4. OS Shell - CLI; interface between OS and User. 
5. Graphics server - provides graphical sub-system (e.g. 'X' or 'X-server').
6. Window Manager - GUI (e.g. GNOME, KDE, MATE, etc.). 
7. Utilities - programs.

Linux can be broken down into layers:

1. Hardware - RAM, CPU, hard drive, etc.
2. Kernel - core of Linux; virtualize and control hardware, allocate memory, etc.; gives each process its own virtual resources and prevents/mitigatees conflicts between different processes.
3. Shell - CLI.
4. System Utility - makes available the OS' functionality. 

Important directories or paths in Linux include: 

* ```/``` - root; top-level directory that contains files required to boot the OS before other file systems are mounted as well as files required to boot other fileshystems. After boot, all other filesystems are mounted at standard mount points as subdirectories of the root.
* ```/bin``` - contains essential command binaries.
* ```/boot``` - static bootloader, kernel executable, and files required to boot Linux.
* ```/dev``` - device files to facilitate access to every hardware device attached to the system.
* ```/etc``` - system config files; also may contain config files for installed apps.
* ```/home``` - each user has subdirectory here for storage.
* ```/lib``` - shared library files required for boot.
* ```/media``` - external removable media (e.g. USB) are mounted here.
* ```/mnt``` - temp mount point for regular filesystems.
* ```/opt``` - optional files (third-party tools can be saved here).
* ```/root``` - home directory for the root user.
* ```/sbin``` - contains executables used for system administration (binary sys files).
* ```tmp``` - temporary file storage; generally cleared on boot.
* ```usr``` - executables, libraries, man files, etc.
* ```var``` - variable files such as log files, email in-boxes, web app related files, cron files, etc.

## Bash

Customization can happen in the shell's configuration file ```.bashrc```.

## System Information

* ```hostname``` - lists computer we are logged into.
* ```whoami``` - current username.
* ```id``` - adds group membership and ids.
* ```uname``` - print system information; ```-r``` can id the kernel for exploits.
* ```pwd``` - working directory.
* ```ifconfig```- network interface.
* ```ip``` - show or manipulate routing.
* ```netstat``` - show network status.
* ```ss``` - utility to investigate sockets.
* ```ps``` - shows process status.
* ```who``` - displays who is logged in.
* ```env``` - prints environment or sets and executes command.
* ```lsblk``` - lists block devices.
* ```lsusb``` - lists usb devices.
* ```lsof``` - lists opened files.
* ```lspci``` - lists pci devices.

## Navigation

* ```cd```  - change directory.
* ```ls``` - list directory contents.
* ```clear``` - clean the shell; also can use ```CRTL + L```.

## Working with Files and Directories

* ```tree``` - lists contents of a directory in a tree-like format.
* ```touch <name>``` - change file timestamps; creates empty file if file does not exist.
* ```mkdir <name>``` - make directories.
* ```mv <file/dir> <renamed file/dir>``` - move (rename) files.
* ```mv <file> <newfilename>``` - rename file by not specifying new directory.
* ```cp <dir/filename> <newdir/filename>``` - copy files and directories.

## Editing Files

```vim``` or ```nano``` are often used for file editing. Note that the ```^``` caret stands for ```CTRL```. 

* ```nano <filename>``` - opens nano editor and creates new file.
* ```vim``` - open vim editor.

```vim``` has a total of six fundamentaal modes that make working with it easier:

1. ```Normal``` - all inputs are considered as editor commands. This is how ```vim``` starts usually.
2. ```Insert``` - characters are entered into the buffer.
3. ```Visual``` - used to mark a contiguous part of the text (highlighted); highlighted are can be deleted, copied, replaced, etc.
4. ```Command``` - allows single-line command at bottom of editor; used for sorting, replacing text sections, or deleting them (e.g.). 
5. ```Replace``` - newly entered text will overwrite existing text. 

Vim has the following actions:

### Moving, Editing, Exiting, Insertion, Appending
* ```hjkl``` - move cursor.
* ```:q!``` - exit vim, trash all changes.
* ```:wq``` - exit vim and save changes.
* ```x``` - delete a character at the cursor.
* ```i``` - insert text before the cursor.
* ```A``` - appendd after the line.
### Deletion, Motions, Count with Motion, Count with Delete, Operating on Lines, Undo
* ```dw``` - delete word (from the cursor up to the next word type).
* ```d$``` - delete from the cursor to the end of a line type.
* ```dd``` - delete the whole line.
* ```2w``` - repeat a mothion based on the prepended number (2 in this case). 
* ```operator number motion``` - change (operator = what to do), (number = count), (motion = moves over the text to operate on (e.g. w - word, $ - end of line)).
* ```0``` - move to the start of the line.
* ```u``` - undo previous action.
* ```U``` - undo all the changes on a line.
* ```CTRL-R``` - undo the undo's.
### Put, Replace, Change, 
* ```p``` - put previously deleted text after the cursor.
* ```rx``` - replace; r sets the cursor, x is the letter to replace the current spot.
* ```ce``` - change until the end of a word; type ```ce``` followed by the replaced text.
* ```c number motion``` - format for change.
### Location, Searching, Matching, Substitution
* ```CTRL-G``` - display your location in the file and the file status.
* ```G``` - moves to the end of the file.
* ```[number] G``` - moves to a specific location in the file (number).
* ```gg``` - moves to the first line.
* ```/ [phrase]``` - searches FORWARD for the phrase.
* ```? [phrase]``` - searches BACKWARD for the phrase. Type ```n``` to find next occurance or ```N``` to go in opposite direction.
* ```CTRL-O``` - takes you back to older positions.
* ```CRTL-I``` - takes you to newer positions.
* ```%``` - when placed on a ```()```, ```[```, or ```{```, it will move to the matching one.
* ```:s/old/new``` - substitute new for the first old in a line type.
* ```:s/old/new/g``` - substitute new for all 'old's on a line type.
* ```:#,#s/old/new/g``` - substitute phrases between two line #'s type.
* ```:%s/old/new/g``` - substitute all occurrences in the file type.
* ```:%s/old/new/gc``` - ask for confirmation each time add 'c'.
### Execute an External Command, Writing Files, Select Text to Write, Retriving/Merging
* ```:![command]``` - execute the command inside Vim.
* ```:w FILENAME``` - save the changes as the new filename.
* ```v motion :w FILENAME``` - save part of the file.
* ```:r FILENAME``` - retrives disk file FILENAME and puts it below the cursor position.
* ```:r !dir``` - reads the output of the dir command and put it below the cursor position.
### Open, Append, Replace, Copy/Paste, Set
* ```o``` - open a line below the cursor and start Insert mode.
* ```O``` - open a line above the cursor.
* ```a``` - insert text after the cursor.
* ```A``` - insert text after the end of the line.
* ```e``` - command moves to the end of a word.
* ```y``` - operator yanks (copies) text, p puts (pastes) it.
* ```R``` - enters replace mode until ```ESC``` is pressed.
* ```:set xxx``` - sets the option ```xxx```.
* ```:set ic``` - ignore upper/lower case when searching.
* ```:set is``` - show partial matches for a search phrase.
* ```:set hls``` - highlight all matching phrases.
* ```no``` - prepend to set a option off.

## Find Files and Directories

* ```which``` - returns the path to the file/link that should be executed; check
if a program exists.
* ```find``` - find files/folders; can filter results (e.g. size, date, etc.).
* ```locate``` - find files by name; to update the database ```locate``` uses, use ```sudo updatedb```.
* ```2>/dev/null``` - hide permission denied files.