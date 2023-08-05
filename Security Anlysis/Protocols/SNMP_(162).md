# <h1 style="text-align:center">Simple Network Management Protocol (SNMP)</h1>

## Introduction
```SNMP``` primarily uses UDP ports 161 and 162. Community strings can provide information/stats about a router or device. Manufacturer default community strings of ```public``` and ```private``` are often unchanged. 


## Helpful Commands

* ```snmpwalk -v 2c -c public <target_IP> ```
* ```snmpwalk -v 2c -c private <target_IP>```

* ```onesixtyone -c dict.txt <target_IP>``` - brute force community string

## Notes

* In version 1 and 2c, access is controlled using a plaintext community string, and if you know the name, you can gain access to it. Encryption/authentication is only needed in SNMP v.3. 


## See Also

```snmpwalk```

```onesixtyone``` - brute force community string names