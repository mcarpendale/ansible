### pb_add_1_config.yml
Configure your Flash Array
- Update Banner
- Set DNS
- Set NTP
- Set individual Host Name for each array in inventory

### pb_add_2_subnet.yml
Add Subnets and VIF for iSCSI-A and iSCSI-B
- SUBNETS
  - MGMT environment: 
    - iSCSI-A - VLAN 3000
    - iSCSI-B - VLAN 3001
  - Customer or Department 1
    - iSCSI-A - VLAN 2000
    - iSCSI-B - VLAN 2001
        Customer or Department 2
    - iSCSI-A - VLAN 2002
    - SCSI-B - VLAN 2003
- VIFs
  - MGMT w/ IPs
    - ct0.eth4.3000 
    - ct1.eth4.3000
    - ct0.eth5.3001
    - ct1.eth5.3001
  - Customer or Department 1 w/ IPs
    - ct0.eth4.2000 
    - ct1.eth4.2000
    - ct0.eth5.2001
    - ct1.eth5.2001
  - Customer or Department 1 w/ IPs
    - ct0.eth4.2002 
    - ct1.eth4.2002   
    - ct0.eth5.2003
    - ct1.eth5.2003       

### pb_add_3_host.yml
Add Host to Host groups
- Hosts
  - Create Hosts
  - Set IQN
  - Set Personality (esxi)
- Host Group
  - Create Host Group
  - Add Host create above

### pb_add_4_datastore.yml
Add DataStore (refer to playbook for execution instructions)
- Create Volume on the Flashg Array
- Add Volume to Host group and set LUN-ID
- Get Volume Info and set NAA Fact
- Rescan one of the ESXi Hosts
- Create Datastore on the ESXi Host
