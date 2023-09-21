# Microsegmentation

1. Fortiswitches must work in the managed mode.
2. disable the set allow-traffic-redirect in the global config of Fortigate 
```
config system global
    set allow-traffic-redirect disable
end
```


3. Block the intra-Vlan traffic under the vlan GW interface 
This is made either in CLI or in GUI:
* GUI:

    * Go to Network > Interfaces.
    * Select the interface and then select Edit.
    * In the Edit Interface form, enable Block intra-VLAN traffic under Network.

* CLI 
```
config system interface
    edit <VLAN name>
        set switch-controller-access-vlan {enable | disable}
    next
end
```



NOTE:

IPv6 is not supported between clients when intra-VLAN traffic blocking is enabled.
Intra-VLAN traffic blocking is not supported when the FortiLink interface type is hardware switch or software switch.




When intra-VLAN traffic blocking is enabled, to allow traffic between hosts, you need to configure the proxy ARP with the config system proxy-arp CLI command and configure a firewall policy. For example:





```
config system proxy-arp
    edit 1
        set interface "V100"
        set ip 1.1.1.1
        set end-ip 1.1.1.200
    next
end
```


```
config firewall policy
    edit 4
        set name "Allow intra-VLAN traffic"
        set srcintf "V100"
        set dstintf "V100"
        set srcaddr "all"
        set dstaddr "all"
        set action accept
        set schedule "always"
        set service "ALL"
    next
end
```