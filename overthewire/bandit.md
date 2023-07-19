
## Bandit 0 -> 1

bandit0 : bandit0

Use ```cat``` to read the ```readme``` file.

    cat readme

## Bandit 1 -> 2

bandit1 : NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL

Specify the full location of the file. A ```-``` is used to specify options / arguments.

    cat ./-
or

    cat < -

## Bandit 2 -> 3

bandit2 : rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi

Use quotation marks when specifying long filenames or paths with spaces. 

    cat "spaces in filename"

## Bandit 3 -> 4

bandit3 : aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG

Show all hidden files with the ```-a``` option. The ```-a``` option tells the system not to ignore entries starting with ```.```.

    ls -a ./inhere

Read the hidden file:

    cat ./inhere/.hidden

## Bandit 4 -> 5

bandit4 : 2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe

Use the ```file``` command to see what types of files there are. 

    cd inhere
    file -- *

```-file07``` is th eonly one that is ASCII text. 

    cat ./-file07

## Bandit 5 -> 6

bandit5 : lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR

    find -size 1033c -type f

## Bandit 6 -> 7

bandit6 : P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU