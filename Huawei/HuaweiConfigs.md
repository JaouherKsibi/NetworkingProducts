# Huawei Configurations 
## Les Routeurs 
---

### Navigate between views
```
<R1>system-view
[R1]quit
<R1>
```
In addition to the quit command, you can also: 
1. Run the return command to return to the user view from any view. 
2. Press Ctrl+Z to return to the user view from any view
### change the Router name 
```
[Router]sysname R1
```
### Help
#### autocomplete
we can enter the first several letters of a keyword in a command and press "tab" 
The first several letters must uniquely identify the keyword.
#### To show the available keywords starting with several letters 
we can enter some letters and the press "?" to show the available commands starting with these several letters 

we can use "space" and then "?" to show the available options

### save configuration 
````
<Datacom-Router>save
``
### display command 
#### to show the VRP version 
```
<R1>display version
```


#### To display the current cofiguration
<R1>display current-configuration

1. Press Ctrl+C or Ctrl+Z to stop the display or command execution. 
2. Press the space bar to display the next screen. 
3. Press Enter to display the next line

#### To display the current cofiguration of the current view
```
display this
```

### To negate a command
```
undo command
```



### assign an ip address to an interface 

```
[Datacom-Router]interface Serial 0/0/0
[Datacom-Router-Serial0/0/0]ip address 192.168.1.1 24
```





### L'utilisation des cables 
On utilise les cables RJ-45 cross-over pour cabler les ports de même type 
On utilise les cables RJ-45 cross through pour connecter les ports de type différent

### Les fibres 
la fibre utilise 2 voies une TX et l'autre RX 
le cablage doit être fait de telle sorte que Tx soit en face de RX et vice versa 




## Establishing Tunnels
### GRE Tunnels

#### For Router1
```

 //Configure a public network outbound interface.
[R1]interface GigabitEthernet1/0/0
[R1-G1/0/0]ip address 3.1.1.1 255.255.255.0

//Configure a tunnel interface and set the source and destination addresses to the IP addresses of interfaces that send and receive packets.

[R1]interface Tunnel0/0/1
[R1-Tunnel0/0/1]ip address 10.4.1.1 255.255.255.0
[R1-Tunnel0/0/1]tunnel-protocol gre
[R1-Tunnel0/0/1]source 3.1.1.1
[R1-Tunnel0/0/1]destination 1.1.1.1
```
#### For Router2

```

[R2]interface GigabitEthernet1/0/0   //Configure a public network outbound interface.
[R2-G1/0/0]ip address 1.1.1.1 255.255.255.0


[R2]interface Tunnel0/0/1   //Configure a tunnel interface and set the source and destination addresses to the IP addresses of interfaces that send and receive packets.
[R2-Tunnel0/0/1]ip address 10.4.1.2 255.255.255.0
[R2-Tunnel0/0/1]tunnel-protocol gre
[R2-Tunnel0/0/1]source 1.1.1.1
[R2-Tunnel0/0/1]destination 3.1.1.1

```



### IPSec Tunnels


#### Manual Configuration with no DPD (Dead Peer Detection)
##### For R1
```
////////////////Router 1/////////////////
acl number 3101
rule 5 permit ip source 10.1.1.0 0.0.0.255 destination 10.1.2.0 0.0.0.255



ipsec proposal tran1  //Configure an IPSec proposal.
 esp authentication-algorithm sha2-256
 esp encryption-algorithm aes-128 

ipsec policy map1 10 manual  //Manually create an IPSec policy.
 security acl 3101
 proposal tran1
 tunnel local 1.1.1.1
 tunnel remote 2.1.1.1
 sa spi inbound esp 54321
 sa string-key inbound esp cipher %^%#JvZxR2g8c;a9~FPN~n'$7`DEV&=G(=Et02P/%\*!%^%#  //Configure authentication key for the inbound SA to huawei.
 sa spi outbound esp 12345
 sa string-key outbound esp cipher %^%#K{JG:rWVHPMnf;5\|,GW(Luq'qi8BT4nOj%5W5=)%^%#  //Configure authentication key for the outbound SA to huawei.



interface GigabitEthernet1/0/0
 ip address 1.1.1.1 255.255.255.0
 ipsec policy map1



ip route-static 10.1.2.0 255.255.255.0 1.1.1.2

```



#####For R2

```
acl number 3101
rule 5 permit ip source 10.1.2.0 0.0.0.255 destination 10.1.1.0 0.0.0.255


ipsec proposal tran1  //Configure an IPSec proposal.
 esp authentication-algorithm sha2-256
 esp encryption-algorithm aes-128 



ipsec policy map1 10 manual  //Manually create an IPSec policy.
 security acl 3101
 proposal tran1
 tunnel local 2.1.1.1 
 tunnel remote 1.1.1.1
 sa spi inbound esp 54321
 sa string-key inbound esp cipher %^%#JvZxR2g8c;a9~FPN~n'$7`DEV&=G(=Et02P/%\*!%^%#  //Configure authentication key for the inbound SA to huawei.
 sa spi outbound esp 12345
 sa string-key outbound esp cipher %^%#K{JG:rWVHPMnf;5\|,GW(Luq'qi8BT4nOj%5W5=)%^%#  //Configure authentication key for the outbound SA to huawei.




interface GigabitEthernet1/0/0
 ip address 2.1.1.1 255.255.255.0
 ipsec policy map1

```

