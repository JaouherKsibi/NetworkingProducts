# Juniper

## Initial Configuration Overview for Juniper Networks Devices
All devices have a version of Junos OS preinstalled.  
Console access to the device is enabled by default. Use a console port to connect to the device initially.  
Remote management access to the device and all management access protocols—such as Telnet, FTP, and SSH—are disabled by default. 

### console port

|  |    |
| :---------------: |:---------------:|
| speed  |   9600 bit rate |
| Data bits  | 8            | 
| Stop bits |    1       | 
| Parity |    none      |  
| Flow Control |    none       | 

1. connect your pc to the console port of the network device 
2. Log in as the user root.
Initially, you won't need a password for the root user account. The device prompt root@% indicates that you are the root user.
3. Type cli to start the Junos OS CLI.
```
root@% cli
root@>
```
4. Type configure to access CLI configuration mode
```
root@> configure
[edit]
root@#
```

### setting up a password for root user 
1. 
```
[edit groups global system]
root@# set root-authentication plain-text-password 
New Password: type password here
Retype new password: retype password here
```
2. 
```
[edit]
root@# set apply-groups group-name
```

3. 
```
root@# commit
```
### configuring hostname



 