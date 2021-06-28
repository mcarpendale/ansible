# Pure Storage Flash Array example playbooks to:

- Configure your Array,
- Create iSCSI Subnets and VIFs
- Add Hosts and Host Group, 
- Create a volume and VMFS Datastore
- Expand the Flash Array Volume and associated VMFS Datastore
- Turn on Remote Assist
- Turn off Remote Assist
- Delete the VMFS Datastore and volume
- Delete the Hosts and Host Group
- Delete the VIFs and Subnets
- Reconfigure your array (in my case, change the login prompt back to what it was)


## Requirements
### The Pure Storage FlashArray collection depends upon:
- Ansible 2.9 or later
- Pure Storage FlashArray system running Purity 4.6 or later
  - some modules require higher versions of Purity
  - some modules require specific Purity versions
- purestorage >=v1.19
- py-pure-client >=v1.14
- Python >=v2.7
- netaddr
- requests
- pycountry

### VMware community collection depends upon following third party libraries:
* Pyvmomi >= 6.7.1.2018.12
* vSphere Automation SDK for Python

## Overview and usage

### pb_add_main.yml
This playbook will complete the 3 actions, by importing plays in `/add`
- Configure your Array
- create iSCSI Subnets and VIFs, 
- add Hosts and Host Group

```
ansible-playbook -i inventory pb_add_main.yml
```


### pb_add_4_datastore.yml
Run this playbook to; 
- create a volume 
- and VMFS Datastore on the esxi host
```
ansible-playbook -i inventory ./add/pb_add_4_datastore.yml -e "array=10.0.0.1 datastore_name=RedDotAC1MikeWasHere datastore_size=2T hg_name=mgmt-esxi lun_id=13"
```


### pb_exp_1_datastore.yml
The expansion play book is used to;
- Increase the Flash Array volume,
- Rescan the esxi host, and
- Expand the VMFS data store using all available free space
```
ansible-playbook -i inventory pb_exp_1_datastore.yml -e "array=10.0.0.1 esxi=mgmt-esx01.purestorage.int datastore_name=RedDotAC1MikeWasHere datastore_size=6T"
```
**NOTE:** this is a new module from `community.vmware.vmware_host_datastore_resize`. Feature request, vmware_host_datastore: Increase capacity #910


### Remote Assist
To turn Remote Assist on `pb_remoteassist_on.yml`
- Turn on for a specific array
```
ansible-playbook -i inventory pb_remoteassist_on.yml -e "array=purefa[0]"
```


To turn Remote Assist off `pb_remoteassist_off.yml`
- Turn off for a specific array
```
ansible-playbook -i inventory pb_remoteassist_off.yml -e "array=purefa[0]"
```

### Cleanup 
To clean up your environment, then run `pb_del_1_datastore.yml` to;
- Delete the VMFS Datastore on the esxi host
- Destroy and *eradicate* the Flash Array Volume
```
ansible-playbook -i inventory ./del/pb_del_1_datastore.yml -e "array=10.0.0.1 datastore_name=RedDotAC1MikeWasHere hg_name=mgmt-esxi"
```

`pb_del_main.yml` will complete the remaining 3 cleanup actions (importing plays from `/del`):
- Delete VIFs and iSCSI Subnets
- Delete Hosts and Host Group
- Re-configure your Array
```
ansible-playbook -i inventory pb_add_main.yml
```
