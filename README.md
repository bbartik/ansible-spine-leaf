## ANSIBLE SPINE-LEAF DEPLOYMENT

This project uses custom ansible roles such as "bgp-leaf" and "bgp-spine" to build out a spine-leaf EVPN network. The logic in the roles is such that all spines peer to leafs and all leafs peer to spines. 


## PREP

*NOTE: Nexus must have "nv overlay evpn" configured before allowing EVPN AF configuration, this does not appear to be in nxos module so perform this step manually*

- Prep each device as follows:

```
conf t
hostname spine1
int mgmt 0
 ip address <mgmt-ip>/<mgmt-mask>
vrf context management
  ip route 0.0.0.0/0 <mgmt-gw>
end
copy running-config startup-config
```

- Install prerequisites:

```
pip install -r requirements
ansible-galaxy collection install -r requirements.yaml -p collection
```

- Update the inventory as needed


## DEPLOY

```
ansible-playbook spine-leaf.yaml
```
