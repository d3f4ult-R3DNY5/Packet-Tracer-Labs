# CCNA Lab 3

>[!NOTE]
>This Project was scrapped as It got overly complicated as i could no achieve my goals of managing the all the devices from a single devices 
>Probably the issue may be one/many/all of the causes 
>1. Due to the native VLAN configuration made 
>2. SVI misconfigurations 
>3. OSPF routes misconfigurations 


# Network Topology 


## Devices 

| DEVICES    | NAME                  |
| ---------- | --------------------- |
| DSW1       | Distribution Switch 1 |
| DSW2       | Distribution Switch 2 |
| ASW1       | Access Switch 1       |
| ASW2       | Access Switch 2       |
| SALES-PC-1 | Sales Department PC   |
| SALES-PC-2 | Sales Department PC   |
| HR-PC-1    | HR Department PC      |
| HR-PC-2    | HR Department PC      |

## Layer 2 Configurations 

### Port-channel configurations 

| Device | Channel - Bundle | protocol/op-mode | Port channel interface |
| ------ | ---------------- | ---------------- | ---------------------- |
| ASW1   | F0/1, F0/2       | LACP passive     | Po1                    |
| DSW1   | F0/1, F0/2       | LACP active      | Po1                    |

---
### VLAN configurations 
Configuring the following VLANS on the devices mentioned below 

```
VLAN 10 - SALES
VLAN 20 - HR
VLAN 30 - MANAGEMENT 
VLAN 99 - NATIVE
VLAN 404 - DISABLED
```

#### Device Assignment 

| Devices    | VLAN assigned |
| ---------- | ------------- |
| SALES-PC-1 | 10            |
| HR-PC-1    | 20            |

#### Trunk configurations 
The following configurations are performed on the trunk ports of ASW1 , ASW2 , DSW1 and DSW2 

>[!NOTE]
>Following Interfaces have been configured on the Above devices 
>- Po1
>- Po2

- **Native VLAN : 99**
- **Allowed VLAN : `[10,20,30,99]`**

---
