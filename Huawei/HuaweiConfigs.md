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