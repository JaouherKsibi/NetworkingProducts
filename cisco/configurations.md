# Configurer un commutateur cisco
## Les configurations de base 
---
### Changer le nom du commutateur
```
Switch> enable
Switch# configure terminal
Switch(config)# hostname S1
S1(config)# exit    
S1#
```
### Sécuriser l'accès à la console par un mot de passe 
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
###
### Configurer l'accès Telnet au commutateur 
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
### Sécuriser l'accès au mode "priviledged EXEC" par un mot de passe 
```
S1> enable
S1# configure terminal
S1(config)# enable password c1$c0
S1(config)# exit
%SYS-5-CONFIG_I: Configured from console by console
S1#
```
### Sécuriser l'accès au mode "priviledged EXEC" par un mot de passe chiffré 
```
S1> enable
S1# configure terminal
S1(config)# enable secret itsasecret
S1(config)# exit
S1#
```
### Enregistrer la configuration 
```
S1> enable
S1# copy running-config startup-config
Destination filename [startup-config]?[Enter]
Building configuration...
[OK]
S1#
```
### Afficher la configuration actuelle
```
S1> enable
S1# show running-config
```
### Afficher la configuration de démarrage
```
S1> enable
S1# show startup-config
```
### Configurer un mot de Bannière:
```
S1> enable
S1# configure terminal
S1(config)#banner motd "Secure System"
```
### Chiffrer tous les mots de passe dans le fichier de configuration
```
S1> enable
S1# configure terminal
S1(config)#service password-encryption
```
