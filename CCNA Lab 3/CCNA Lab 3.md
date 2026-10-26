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





