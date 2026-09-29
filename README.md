# OSPF-Single-area-LAB

A simple lab where three Cisco routers run OSPF Area 0 so two remote LANs can reach each other without static routes.


Addressing
Device	IP Address	Connected To
PC0    	192.168.10.10/24	Switch0 → R1
R1	    192.168.10.1/24 (LAN), 10.0.12.1/30	R2
R2	    10.0.12.2/30, 10.0.23.1/30	R1, R3
R3	    10.0.23.2/30, 192.168.30.1/24 (LAN)	R2
PC1	    192.168.30.10/24	Switch1 → R3


OSPF Configuration :

R1

router ospf 1
 network 192.168.10.0 0.0.0.255 area 0
 network 10.0.12.0 0.0.0.3 area 0

R2

router ospf 1
 network 10.0.12.0 0.0.0.3 area 0
 network 10.0.23.0 0.0.0.3 area 0

R3

router ospf 1
 network 10.0.23.0 0.0.0.3 area 0
 network 192.168.30.0 0.0.0.255 area 0

 
Verify : 
show ip ospf neighbor
show ip route ospf
PC0> ping 192.168.30.10

Neighbors should show FULL, and the ping from PC0 to PC1 should succeed.
