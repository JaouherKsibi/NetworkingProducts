# Les produits réseau de Cisco 
## Configurer un commutateur cisco
### Les configurations de base 
---
#### Changer le nom du commutateur
```
Switch> enable
Switch# configure terminal
Switch(config)# hostname S1
S1(config)# exit    
S1#
```
#### Sécuriser l'accès à la console par un mot de passe 
```
S1> enable
S1# configure terminal
S1(config)# line console 0
S1(config-line)# password letmein
S1(config-line)# login
S1(config-line)# exit
S1(config)# exit
%SYS-5-CONFIG_I: Configured from console by console
S1#
```
####
#### Configurer l'accès Telnet au commutateur 
```
S1> enable
S1# configure terminal
S1(config)# line vty 0 15
S1(config-line)# password letmein
S1(config-line)# login
S1(config-line)# exec-timeout 15
S1(config-line)# exit
%SYS-5-CONFIG_I: Configured from console by console
S1#
``` 
#### Sécuriser l'accès au mode "priviledged EXEC" par un mot de passe 
```
S1> enable
S1# configure terminal
S1(config)# enable password c1$c0
S1(config)# exit
%SYS-5-CONFIG_I: Configured from console by console
S1#
```
#### Sécuriser l'accès au mode "priviledged EXEC" par un mot de passe chiffré 
```
S1> enable
S1# configure terminal
S1(config)# enable secret itsasecret
S1(config)# exit
S1#
```
#### Enregistrer la configuration 
```
S1> enable
S1# copy running-config startup-config
Destination filename [startup-config]?[Enter]
Building configuration...
[OK]
S1#
```
#### Afficher la configuration actuelle
```
S1> enable
S1# show running-config
```
#### Afficher la configuration de démarrage
```
S1> enable
S1# show startup-config
```
#### Configurer un mot de Bannière:
```
S1> enable
S1# configure terminal
S1(config)#banner motd "Secure System"
```
#### Chiffrer tous les mots de passe dans le fichier de configuration
```
S1> enable
S1# configure terminal
S1(config)#service password-encryption
```



## Configuration d'un firewall cisco ASA 

### change the fw mode 
#### transport mode 
```
hostname(config)# firewall transparent
```
#### routed mode 
```
hostname(config)# no firewall transparent
```


## configuring ARP inspection in the transparent firewall 
To configure ARP Inspection, perform the following steps:
Step 1: Add static ARP entries
```
arp interface_name ip_address mac_address

hostname(config)# arp outside 10.1.1.1 0009.7cbe.2100
```
Step 2: Enable ARP inspection 

```
arp-inspection interface_name enable [ flood | no-flood ]

hostname(config)# arp-inspection outside enable no-flood

```
"no flood" drops the non-matching packets 
"flood"  forwards non matchingpackets on all other interfaces 

## Customizing the MAC Address Table for the Transparent Firewall

### Adding a Static MAC Address
```
mac-address-table static interface_name mac_address

 mac-address-table aging-time timeout_value_in_minutes

 
hostname(config)# mac-address-table static inside 0009.7cbe.2100
hostname(config)# mac-address-table aging-time 10 
```


### Disabling MAC Address Learning

```
mac-learn interface_name disable
 
hostname(config)# mac-learn inside disable
```

## Monitoring the Transparent Firewall
### Monitoring ARP Inspection
```
show arp-inspection
```
Shows the current settings for ARP inspection on all interfaces.


### Monitoring the MAC Address Table


```
show mac-address-table [ interface_name ]

```

## Security Context 

in multiple context mode, dynamic routing, multicast and VPN are not supported
Multicast or broadcast traffic is duplicated and delivered to each context.
### Enabling Multiple Context Mode 
```
hostname(config)# mode multiple
```
You are prompted to reboot the security appliance.

### Restoring Single Context Mode

Step 1 Copy the backup version of your original running configuration to the current startup configuration:
```
hostname(config)# copy flash:old_running.cfg startup-config
```


Step 2 Set the mode to single mode:
```
hostname(config)# mode single
```
The security appliance reboots.



### Configuring a Security Context
#### Step 1 To add or modify a contex
```
hostname(config)# context name
```

#### Step 2 (Optional) To add a description for this context

```
hostname(config-ctx)# description text
```

#### Step 3 To specify the interfaces you can use in the context
```
hostname(config-ctx)# allocate-interface physical_interface [map_name] [visible | invisible]
```