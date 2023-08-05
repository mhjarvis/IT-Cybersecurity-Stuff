# <h1 style="text-align:center">Remote Desktop Protocol</h1>

## Introduction

Remote Desktop Protocol (RDP) is used for remote desktop sessions and operates on ports ```3389 TCP``` and ```3389 UDP```. 

## Links

[SpeedGuide.net Port 3389](https://www.speedguide.net/port.php?port=3389)

## ```xfreerdp```
```xfreerdp``` is an X11 Remote Desktop Protocol (RDP) client. 

    xfreerdp [file] [options] [/v:server[:port]]

    xfreerdp /v:{target_IP}     // test gues login capabilities

## Options

    /cert:ignore        // specifies that all security certificate usage should be ignored.
    /u:Administrator    