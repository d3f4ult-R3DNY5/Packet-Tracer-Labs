# Development Team 

## Diagram 

![](../images/DEVELOPMENT-TEAM.drawio.svg)

---

## IP Diagram 

![](../images/DEVELOPMENT-TEAM-IP-DIAGRAM.drawio.svg)

---

## LAYER 2 configurations 

### Port channels configurations 

#### DEV AS 1 & DEV AS 2

| Port channel Name | Ports             | Destination |
| ----------------- | ----------------- | ----------- |
| Po1               | Fa0/5(P) Fa0/6(P) | DEV-ALS-1   |

#### DEV ALS 1 

| Port channel Name | Ports                                  | Destination |
| ----------------- | -------------------------------------- | ----------- |
| Po1               | Fa0/1(P) Fa0/2(P)                      | DEV-AS-1    |
| Po2               | Fa0/3(P) Fa0/4(P)                      | DEV-AS-2    |
| Po3               | Fa0/5(P) Fa0/6(P) Fa0/7(P) Fa0/8(P)    | DEV-DS-1    |
| Po4               | Fa0/9(P) Fa0/10(P) Fa0/11(P) Fa0/12(P) | DEV-DS-2    |
#### DEV AS 3 & DEV AS 4

| Port channel Name | Ports             | Destination |
| ----------------- | ----------------- | ----------- |
| Po1               | Fa0/5(P) Fa0/6(P) | DEV-ALS-2   |

#### DEV ALS 2

| Port channel Name | Ports                                  | Destination |
| ----------------- | -------------------------------------- | ----------- |
| Po1               | Fa0/1(P) Fa0/2(P)                      | DEV-AS-3    |
| Po2               | Fa0/3(P) Fa0/4(P)                      | DEV-AS-4    |
| Po3               | Fa0/5(P) Fa0/6(P) Fa0/7(P) Fa0/8(P)    | DEV-DS-2    |
| Po4               | Fa0/9(P) Fa0/10(P) Fa0/11(P) Fa0/12(P) | DEV-DS-1    |

#### DEV DS 1

| Port channel Name | Ports                                           | Destination |
| ----------------- | ----------------------------------------------- | ----------- |
| Po1               | Gig1/0/1(P) Gig1/0/2(P) Gig1/0/3(P) Gig1/0/4(P) | DEV-ALS-1   |
| Po2               | Gig1/0/5(P) Gig1/0/6(P) Gig1/0/7(P) Gig1/0/8(P) | DEV-ALS-2   |
| Po3               | Gig1/0/9(P) Gig1/0/10(P)                        | DEV-CS-1    |

#### DEV DS 2

| Port channel Name | Ports                                           | Destination |
| ----------------- | ----------------------------------------------- | ----------- |
| Po1               | Gig1/0/1(P) Gig1/0/2(P) Gig1/0/3(P) Gig1/0/4(P) | DEV-ALS-2   |
| Po2               | Gig1/0/5(P) Gig1/0/6(P) Gig1/0/7(P) Gig1/0/8(P) | DEV-ALS-1   |
| Po3               | Gig1/0/9(P) Gig1/0/10(P)                        | DEV-CS-1    |
#### DEV CS 1

| Port channel Name | Ports                   | Destination |
| ----------------- | ----------------------- | ----------- |
| Po1               | Gig1/0/1(P) Gig1/0/2(P) | DEV-DS-1    |
| Po2               | Gig1/0/3(P) Gig1/0/4(P) | DEV-DS-2    |
| Po3               | Gig1/0/5(P) Gig1/0/6(P) | DEV-CS-2    |

#### DEV CS 2

| Port channel Name | Ports                   | Destination |
| ----------------- | ----------------------- | ----------- |
| Po1               | Gig1/0/1(P) Gig1/0/2(P) | DEV-DS-1    |
| Po2               | Gig1/0/3(P) Gig1/0/4(P) | DEV-DS-2    |
| Po3               | Gig1/0/5(P) Gig1/0/6(P) | DEV-CS-2    |
#### DEV CS 2

| Port channel Name | Ports                   | Destination |
| ----------------- | ----------------------- | ----------- |
| Po1               | Gig1/0/1(P) Gig1/0/2(P) | DEV-CS-1    |

### Access Ports and VLAN 

| ACESS PORT | VLAN | DEVICES |
| ---------- | ---- | ------- |
|            |      |         |
