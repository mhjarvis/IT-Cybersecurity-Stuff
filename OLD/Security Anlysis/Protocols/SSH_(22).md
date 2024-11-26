# <h1 style="text-align:center">Secure Shell (SSH)</h1>

## Introduction
Secure Shell (SSH) is a network protocol that runs on port 22 by default and is used primarily for secure remote access.SSH can be configured with password authentication or passwordless using public-key authentication using an SSH public/private key pair. SSH can be used to remotely access systems on the same network, over the internet, facilitate connections to resources in other networks using port forwarding/proxying, and upload/download files to and from remote systems.

SSH uses a client-server model. SSH is typically more stable than a reverse shell connection and may be used as a 'jump host' to enumerate and attack other hosts. With credentials, we can login remotely using the ```username@remoteserverIP```.

    ssh bob@10.10.10.10

Its also possible to read local private keys on a compromised system or add our public key to gain SSH access to a specific user. 

### Private Key
If able to obtain a private key, after adding to your .ssh folder, it should be possible to log in as the user that ssh key belongs to.