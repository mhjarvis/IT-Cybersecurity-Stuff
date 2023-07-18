<h1 style="text-align: center">Getting Stated with the Basics</h1>

## The Linux Filesystem

    /root - home directory of the root user
    /etc - contains the Linux configuration files ( controls how programs start)
    /home - user's home directory
    /mnt - where other filesystems are attached or mounted to the filesystem
    /media - where cds and usb devices are attached / mounted to the filesystem
    /bin - application binaries reside here
    /lib - libraries

## Basic Commands

    pwd - shows where you are currently located
    whoami - shows which user you are loggd in as
    cd - use to move between directories
    cd ../.. - move up two levels
    ls - see contents of a directory  (list)
        -l - gets more info about files (long listing)
        -a - shows hidden files
        --help / -h / ? - show the dedicated help file
    man - shows the referencing manual
    locate [keyword] - will go through entire filesystem and locate every occurence of that word
    whereis [keyword] - returns location, source, and man page of the binary
    which [keyword] - returns location of binaries in teh PATH variable in Linux

    find [directory] [option] [expression] - e.g (find / -type f -name apache2)

## Wildcards

    ? - respresents a single character
    [] - wildcard matches the letters inside the array
    * - matches any character of any length

## Filtering with ```grep```

```grep``` is often used when output is piped from one command to another. In other words, we can take the output of one command and send it as input to another command. We use the ```|``` to do this.

    ps - displays information about processes running on the machine
    ps aux - provides a listing of all process running in the system

Using ```grep``` we can narrow down the list of processes to see if specific processes are running. For example:

    ps aux

## Creating 

    cat > [filename] - creates a new file and will go into interactive mode; ctrl-D will exit the prompt

    cat >> [filename] - append additional text
    cat > [filename] - will overwrite if file exists

    touch [filename] - create new file
    mkdir [newdirectory] - create new directory
    cp oldfile [directory for newfile] - copy file to new directory

When copying the new file, renaming is optional. 

    mv newfile [directory] - move file without copying
    mv newfile newfile2 - rename file

    rm [filename] - remove a file
    rmdir [directoryname] remove directory (must be empty)
    rmdir -r [directoryname] - removes directory even with file in it

<h1 style="text-align: center">Text Manipulation</h1>

    head [filename] - by default, show the first 10 lines of a file
    head -20 [filename] - display the first 20 lines
    tail [filename] - last 10 lines of a file
    tail -20 [filename] 0 display the last 20 lines

## Numbering Lines

    nl [directory location] - provide line numbers (nl paswd)
    sed - stream editor; find and replace

For working with larger files you have the ```more``` and ```less``` commands.

    more [filename] - display a page of the file at a time, page through with ENTER
    less [filename] - adds ability to filter output by terms
        / - provides prompt to search for keywords
        n - goes to the next occurence of the pattern

<h1 style="text-align: center"></h1>





<h1 style="text-align: center"></h1>
<h1 style="text-align: center"></h1>
<h1 style="text-align: center"></h1>
<h1 style="text-align: center"></h1>
<h1 style="text-align: center"></h1>
<h1 style="text-align: center"></h1>
<h1 style="text-align: center"></h1>
<h1 style="text-align: center"></h1>
<h1 style="text-align: center"></h1>
<h1 style="text-align: center"></h1>
