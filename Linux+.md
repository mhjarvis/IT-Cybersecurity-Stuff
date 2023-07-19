<h1 style='text-align:center'>Basics</h1>

## The Kernel

The kernel layer is the core of the operating system and most Linux distros use a monolithic kernel (some GNUs use a microkernel). The kernel also connects applications to the operating system. 

## Administrator Rights

```su``` stands for switch user, with the default being root. The ```sudo``` commands allows you to run a single command with ```root``` privelages. The advantages of ```sudo``` is that you do not need to know the ```root``` password and you don't stay logged in as ```root```. Use ```exit``` to exit ```root```.

The ```passwd``` command is used to change your password. ```passwd -S``` display user account status information.