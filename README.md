!!! READ !!!

- Nexus must have "nv overlay evpn" configured before allowing evpn af configuration, this does not appear to be in nxos module
- Prep the devices as follows:

spine1:

conf t
hostname spine1
int mgmt 0
 ip address 172.28.87.61/24
vrf context management
  ip route 0.0.0.0/0 172.28.87.1
end
copy running-config startup-config

spine2:

conf t
hostname spine2
int mgmt 0
 ip address 172.28.87.62/24
vrf context management
  ip route 0.0.0.0/0 172.28.87.1
end
copy running-config startup-config

leaf1:

conf t
hostname leaf1
int mgmt 0
 ip address 172.28.87.63/24
vrf context management
  ip route 0.0.0.0/0 172.28.87.1
end
copy running-config startup-config

leaf2:

conf t
hostname leaf2
int mgmt 0
 ip address 172.28.87.64/24
vrf context management
  ip route 0.0.0.0/0 172.28.87.1
end
copy running-config startup-config