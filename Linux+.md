<h1 style='text-align:center'>Basics</h1>

## The Kernel

The kernel layer is the core of the operating system and most Linux distros use a monolithic kernel (some GNUs use a microkernel). The kernel also connects applications to the operating system. 

## Administrator Rights

```su``` stands for switch user, with the default being root. The ```sudo``` commands allows you to run a single command with ```root``` privelages. The advantages of ```sudo``` is that you do not need to know the ```root``` password and you don't stay logged in as ```root```. Use ```exit``` to exit ```root```.

The ```passwd``` command is used to change your password. ```passwd -S``` display user account status information.

## Application Software

### The ```ls``` Command
```ls``` will list files in the current directory. With the ```ls -F``` option will show the file type:

    / - denotes directory
    @ - shortcut
    * - executable file

### The ```history``` and ```who``` Commands

```history``` will show a list of commands just ran. You can use ```!``` followed by a number to then run that command again. Or you can begin to type the command and it will match based on characters. The ```who``` command shows who is currently logged in to the system and which terminal they are using.

### The ```echo```, ```cat```, and ```more``` Commands

```echo``` is used to see how arguments will appear, to create a file, or to modify a file. You can use the ```>``` as a redirect to save a file, etc. The ```more``` command dumps out a page at a time instead of all at once as with ```cat```. Use ```Enter``` to scroll a line at a tim or ```Spacebar``` to scroll to another page.

    / - makes the next character literal (e.g. makes `Enter` a carriage return)
    # - means comment

### The ```man```, ```whatis```, and ```apropos``` Commands

The ```man``` commands for the respective manual. ```man``` uses ```more``` command featuresf. There are a total of eight sections into which ```man``` pages are divided into:

    1. commands any user can run
    2. system calls
    3. library functions
    4. special files
    5. configuration file formats
    6. games
    7. miscellaneous
    8. administrative user commands

If you are not able to access a search engin, you have ```whatis``` and ```apropos```. Both commands search the ```man``` page. ```apropos``` searches both the command field and the short description field for nay match. The ```whatis``` command searches only the command field for an exact match.