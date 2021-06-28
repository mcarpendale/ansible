# Example playbooks to:

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

## Overview and usage

### pb_add_main.yml
This playbook will complete the 3 actions, by importing plays in `/add`
- Configure your Array
- create iSCSI Subnets and VIFs, 
- add Hosts and Host Group

```ansible-playbook -i inventory pb_add_main.yml```


### pb_add_4_datastore.yml
Run this playbook to; 
- create a volume 
- and VMFS Datastore on teh esxi host

```ansible-playbook -i inventory ./add/pb_add_4_datastore.yml -e "array=10.0.0.1 datastore_name=RedDotAC1MikeWasHere datastore_size=2T hg_name=mgmt-esxi lun_id=13"```

**NOTE:** additional variables required in CLI with `-e`


### pb_exp_1_datastore.yml
The expansion play book is used to;
- Increase the Flash Array volume,
- Rescane the esxi host, and
- Expand the VMFS data store using all available free space

```ansible-playbook -i inventory pb_exp_1_datastore.yml -e "array=10.0.0.1 esxi=mgmt-esx01.purestorage.int datastore_name=RedDotAC1MikeWasHere datastore_size=6T"```

**NOTE:** this is a new module from `community.vmware.vmware_host_datastore_resize`. Feature request, vmware_host_datastore: Increase capacity #910

### Remote Assist
To turn Remote Assist on `pb_remoteassist_on.yml`
- Turun on for a specific array

```ansible-playbook -i inventory pb_remoteassist_on.yml -e "array=purefa[0]"```


To turn Remote Assist off `pb_remoteassist_off.yml`
- Turun off for a specific array

```ansible-playbook -i inventory pb_remoteassist_off.yml -e "array=purefa[0]"```

### Claenup 
To clean up your environment, then run `pb_del_1_datastore.yml` to;
- Create a volume 
- Delete the VMFS Datastore on the esxi host
- Destroy and *eradicate* the Flash Array Volume

```ansible-playbook -i inventory ./del/pb_del_1_datastore.yml -e "array=10.0.0.1 datastore_name=RedDotAC1MikeWasHere hg_name=mgmt-esxi"```

`pb_del_main.yml` will complete the remaining 3 cleanup actions:
- Delete VIFs and iSCSI Subnets
- Delete Hosts and Host Group
- Re-configure your Array

    ansible-playbook -i inventory pb_add_main.yml
