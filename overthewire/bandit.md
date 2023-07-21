# Logon
ssh -p 2220 bandit1@bandit.labs.overthewire.org

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

```tr``` will allow us to pick and choose how to translate lowercase/uppercase values. In this case, we offset everything by 13 letters. 

    cat data.txt | tr '[a-zA-Z]' '[n-za-mN-ZA-M]'

## Bandit 12 -> 13

bandit12 : JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv

Create a directory under ```tmp``` and copy the file into the new directory to work with. 

    mkdir /tmp/marku
    cp data.txt /tmp/marku
    cd /tmp/marku

We can reverse the hexdump and revert it to a new file:

    xxd -revert original.txt > test
    file test           // gzip compressed data, was 'data2.bin'
-a
Continue the decompression, checking the file each time.

    mv test data.gz     // rename into gzip file type
    gzip -d data.gz     // unzip - gives us a data file

The file has been compressed multiple times using multiple compression methods. Continue to decompress each file, check what type of file each is and how it was decompressed, until finally you get the ASCII text file as a result. 

    bzip2 -dc data > test   // using bzip2 for decompression
    gzip -d 1.gz            // using gzip for decompression
    tar -xf [filename]      // using tar for decompression


## Bandit 13 -> 14

bandit13 : wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw

Begin by getting the RSA key.

    cat sshkey.private

Use the ```-i``` option to log into the server with the private key.

    ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220

## Bandit 14 -> 15

bandit14 : fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq

    nc localhost 30000
    fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq

Another approach is to use ```telnet``` to connect. Do so by inputing the ```localhost``` and port number:

    telnet localhost 30000

```telnet``` is short for Telecommunication network. It provides remote access to other hosts using the CLI. It normally uses port 23, however, keep in mind that it is insecure and a deprecated protocol. ```telnet``` sends all data in clear text, including usernames and passwords. 

## Bandit 15 -> 16

bandit15 : jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt

    openssl s_client -connect localhost:30001
    jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt

For a deeper understanding, see https://www.misterpki.com/openssl-s-client/


## Bandit 16 -> 17

bandit16 : JQttfApK4SeyHwDlI9SXGR50qclOAil1

    nmap -p31000-32000 localhost

This gives us the following private key:

    MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
    imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
    Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
    DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
    JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
    x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
    KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
    J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
    d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
    YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
    vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
    +TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
    8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
    SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
    HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
    SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
    R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
    Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
    R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
    L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
    blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
    YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
    77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
    dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
    vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=

Create a new directory /tmp/key and save the key there. Then we can ssh into the next level:

    ssh -i private.key bandit17@bandit.labs.overthewire.org -p 2220

    or 

    ssh -i private.key bandit17@localhost

    cat /etc/bandit_pass/bandit17

## Bandit 17 -> 18

bandit17 : VwOSWtCA7lRKkTfbr2IDh6awj9RNZM5e

```diff``` allows us to compare files line by line. 

    diff [OPTION]... [FILES]

    diff --normal passwords.new passwords.old

We get the following output and will want the first password presented since this is the change in the password.new file.

    42c42
    < hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg
    ---
    > glZreTEH1V3cGKL6g4conYqZqaEj0mte

## Bandit 18 -> 19

bandit18 : hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg