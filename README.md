## ANSIBLE SPINE-LEAF DEPLOYMENT

This project uses custom ansible roles such as "bgp-leaf" and "bgp-spine" to build out a spine-leaf EVPN network. The logic in the roles is such that all spines peer to leafs and all leafs peer to spines. 


## PREP

- Nexus must have "nv overlay evpn" configured before allowing evpn af configuration, this does not appear to be in nxos module

Prep the devices as follows:

spine1:
```
conf t
hostname spine1
int mgmt 0
 ip address 172.28.87.61/24
vrf context management
  ip route 0.0.0.0/0 172.28.87.1
end
copy running-config startup-config
```

spine2:
```
conf t
hostname spine2
int mgmt 0
 ip address 172.28.87.62/24
vrf context management
  ip route 0.0.0.0/0 172.28.87.1
end
copy running-config startup-config
```

leaf1:
```
conf t
hostname leaf1
int mgmt 0
 ip address 172.28.87.63/24
vrf context management
  ip route 0.0.0.0/0 172.28.87.1
end
copy running-config startup-config

leaf2:
```
conf t
hostname leaf2
int mgmt 0
 ip address 172.28.87.64/24
vrf context management
  ip route 0.0.0.0/0 172.28.87.1
end
copy running-config startup-config
```

## DEPLOY

```
pip install -r requirements
ansible-galaxy collection install -r requirements.yaml -p collections
ansible-playbook spine-leaf.yaml
```