# CCNA Lab 3

>[!NOTE]
>This lab was built in pursuit of my CCNA Certification Learning and Tries to mimic the real world scenarios as closely as possible 


## Scenario 

- Basic Setup for a SOHO environment for an Enterprise A with several network functions which includes 
	- routing 
	- FTP 
	- DNS
	- DHCP 
	- NTP 

>[!note]
>This based on best of my knowledge

---
## Lab Topology 

<img src="topology.png" width="auto">

---

## Layer 2 configurations 

### VLAN configurations 

On the following switches i.e. `ASW1 ASW2 ASW3 ASW4` `DSW1 DSW2 DSW3 DSW4` `MGMSW1 CONSW1` the following VLAN's will be created 
- VLAN 99 : Management VLAN 
- VLAN 100 : Sales 
- VLAN 200 : Logistics 
- VLAN 404 : Disabled 

### Configuring Access ports in the proper VLAN 

| PC names           | VLAN |
| ------------------ | ---- |
| PC1, PC3, PC5, PC7 | 100  |
| PC2, PC4, PC6, PC8 | 200  |

>[!NOTE]
>For safety I have moved all of the unused ports in VLAN 404 and have disabled it 

### Channel group configurations 

| channel group | port channel | interfaces | mode                 | device(s)                 |
| ------------- | ------------ | ---------- | -------------------- | ------------------------- |
| 1             | Po1          | F0/3-4     | LACP passive , Trunk | ASW1 , ASW2 , ASW3 , ASW4 |
| 2             | Po2          | F0/5-6     | LACP passive , Trunk | ASW1 , ASW2 , ASW3 , ASW4 |
| 1             | Po1          | F0/1-2     | LACP active , Trunk  | DSW1 , DSW2 , DSW3 , DSW4 |
| 2             | Po2          | F0/3-4     | LACP active , Trunk  | DSW1 , DSW2 , DSW3 , DSW4 |
>[!NOTE]
>Configuring all the Port channel to use the load balancing of SRC-DST-IP 


### Configuring to use STP 

For the purpose of this networking LAB , The STP operating mode will will be the classic spanning tree ieee
- `spanning-tree vlan [id] root primary ` has been configured on DSW1 and DSW3 for **VLAN 1 , 99 , 100 , 200**
- `spanning-tree vlan [id] root secondary ` has been configured on DSW2 and DSW4 for **VLAN 1 , 99 , 100 , 200**
- Spanning tree root guard has been configured on the Po1 and Po2 interfaces of DSW1 and DSW3
- Spanning tree portfast has been configured on the following interfaces F0/1-2 on `ASW1 ASW2 ASW3 ASW4` For quick transitioning to the forwarding state 


---

## Layer 3 configurations 

### Port-channel lad balancing method 
- Configuring the port channel load balancing method to be source and destination IP  

### SVI Configurations for VLAN 100 and VLAN 200 

| Interface | IP configurations | Subnet mask     | Devices |
| --------- | ----------------- | --------------- | ------- |
| VLAN 100  | 10.0.1.2          | 255.255.255.128 | DSW1    |
| VLAN 200  | 10.0.1.130        | 255.255.255.128 | DSW1    |
| VLAN 100  | 10.0.1.3          | 255.255.255.128 | DSW2    |
| VLAN 200  | 10.0.1.131        | 255.255.255.128 | DSW2    |
| VLAN 100  | 10.0.2.2          | 255.255.255.128 | DSW3    |
| VLAN 200  | 10.0.2.130        | 255.255.255.128 | DSW3    |
| VLAN 100  | 10.0.2.3          | 255.255.255.128 | DSW4    |
| VLAN 200  | 10.0.2.131        | 255.255.255.128 | DSW4    |

### Connections between CR1 and `[DSW1 , DSW2]`

| Interface | IP configurations | Subnet mask     | Devices | Default Gateway |
| --------- | ----------------- | --------------- | ------- | --------------- |
| G0/1      | 172.16.0.2        | 255.255.255.248 | DSW1    | 172.16.0.1      |
| G0/1      | 172.16.0.3        | 255.255.255.248 | DSW2    | 172.16.0.1      |
| G0/0/0    | 172.16.0.1        | 255.255.255.248 | CR1     | N/A             |


### Connections between CR2 and `[DSW3 , DSW4]`

| Interface | IP configurations | Subnet mask     | Devices | Default Gateway |
| --------- | ----------------- | --------------- | ------- | --------------- |
| G0/1      | 172.16.1.2        | 255.255.255.248 | DSW1    | 172.16.0.1      |
| G0/1      | 172.16.1.3        | 255.255.255.248 | DSW2    | 172.16.0.1      |
| G0/0/0    | 172.16.1.1        | 255.255.255.248 | CR1     | N/A             |

### Connections between CR1 CSW1 & CR2

| Interface | IP configurations | Subnet mask     | Devices |
| --------- | ----------------- | --------------- | ------- |
| G1/0/1    | 172.16.2.1        | 255.255.255.248 | CSW1    |
| G1/0/2    | 172.16.2.9        | 255.255.255.248 | CSW2    |
| G0/0/1    | 172.16.2.2        | 255.255.255.248 | CR1     |
| G0/0/1    | 172.16.2.10       | 255.255.255.248 | CR2     |

### Configuring the management IP 

| Interface  | IP configurations | Subnet mask     | Devices | Default Gateway |
| ---------- | ----------------- | --------------- | ------- | --------------- |
| vlan 99    | 192.168.100.1     | 255.255.255.0   | CSW1    | NA              |
| vlan 99    | 192.168.100.2     | 255.255.255.0   | CONSW1  | 192.168.100.1   |
| Loopback 0 | 192.168.100.100   | 255.255.255.255 | CR1     | NA              |
| Loopback 0 | 192.168.100.200   | 255.255.255.255 | CR2     | NA              |
| vlan 99    | 192.168.100.101   | 255.255.255.0   | CONSW2  | 192.168.100.100 |
| vlan 99    | 192.168.100.201   | 255.255.255.0   | CONSW3  | 192.168.100.200 |
| vlan 99    | 192.168.100.102   | 255.255.255.0   | DSW1    | NA              |
| vlan 99    | 192.168.100.103   | 255.255.255.0   | DSW2    | NA              |
| vlan 99    | 192.168.100.104   | 255.255.255.0   | ASW1    | 192.168.100.1   |
| vlan 99    | 192.168.100.105   | 255.255.255.0   | ASW2    | 192.168.100.1   |
| vlan 99    | 192.168.100.202   | 255.255.255.0   | DSW3    | NA              |
| vlan 99    | 192.168.100.203   | 255.255.255.0   | DSW4    | NA              |
| vlan 99    | 192.168.100.204   | 255.255.255.0   | ASW3    | 192.168.100.1   |
| vlan 99    | 192.168.100.205   | 255.255.255.0   | ASW4    | 192.168.100.1   |

### Configuring the multi area OSPF 
#### Devices participating in the OSPF

#### Area 1 

>- DSW1
>- DSW2
>- CR1

#### Area 2

>- DSW3
>- DSW4
>- CR2

#### Area 0 

>- CR1
>- CR2
>- CSW1


