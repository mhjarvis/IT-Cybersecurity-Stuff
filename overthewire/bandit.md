
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

    find -size 1033c -type f ! -executable

## Bandit 6 -> 7

bandit6 : P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU

Use ```2>/dev/null``` to hide all error messages in the output. 

    find -size 33c -group bandit6 -user bandit7 2>/dev/null

## Bandit 7 -> 8

bandit7 : z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S

Use grep to filter content via piping.

    cat data.txt | grep millionth

## Bandit 8 -> 9

bandit8 : TESKZC0XvTetK0S9xNwm25STk5iWrBvP

First, use ```sort``` with the ```-n``` option to sort based on numerical values. Then, we can pipe it into the ```uniq``` command. With the ```-u``` option, we will print only the uniq value.

    sort -n data.txt | uniq -u

## Bandit 9 -> 10

bandit9 : EN632PlfYiZbn3PhVK3XOGSlNInNE00t

```strings``` will print the printable character sequences that are at least 4 characters long. We know that there are several '=' characters preceeding it, so we could pipe the result of ```strings``` to ```grep``` and simply search for that sequence. 

    strings data.txt | grep ===*

## Bandit 10 -> 11

bandit10 : G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s

```base64``` can encode or decod a file or standard input/output. Use the ```-d``` option to decode data. 

    base64 -d data.txt

## Bandit 11 -> 12

bandit11 : 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM