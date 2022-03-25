# Pure Storage Flash Array NON Disruptive Volume Migration demo
This NON Disruptive Volume Migration demo/example for vSphere or esxi builds off the work Simon has done [`here`](https://github.com/PureStorage-OpenConnect/ansible-playbook-examples/tree/master/flasharray/live-migration)


This playbook will
- Prepare the environment
- Deploy a VM to the migration Datastore
- Migrate the volume (`non disruptively`)
- Clean up the environment

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
- Pyvmomi >= 6.7.1.2018.12
- vSphere Automation SDK for Python

### Hardware
- 2 x FlashArray (source and destination) with iSCSI connectivity, on the same VLAN
- FlashArray's capable of being connected in an ActiveCluster
- Host with iSCSI connectivity on same VLAN as FlashArray iSCSI network

## Pre-Requisites
- Update the ``vars.yaml`` file with the correct for the source and destination array
``` YAML
src_array_ip: 10.0.0.1
src_array_api: 84f1db69-0000-1111-2222-33333333333d
dst_array_ip: 10.0.0.2
dst_array_api: 84f1db69-0000-1111-2222-33333333333e
  ```

## Running the demo/example
To create the example volume used in the main migration run the following playbook:
> `1_prepare-vol.yaml`

To to deploy a VM so the VMFS Datastore has IO, run;:
> `2_deploy-vm-for-migration.yaml`

To perform the actual data migration run:
> `3_migrate-vol.yaml`

To remove all parts of this demo after successful completion run:
> `4_cleanup.yaml`

To remove the Demo VM run:
> `5_deploy-vm-fail-clean.yaml`

You can clean up a `failed` prepare with:
> `6_prepare-fail-clean.yaml`

If the migration `fails` you can use the below playbook to clean up your environment;
> `7_migration-fail-clean.yaml`

## Enhancements
At some point I'll add in the following
- deploy VM to the datastore/volume being migrated - `added` Friday 25 March 2022
- execute random write command on the VM to introduce load and show Active Cluster mirrored writes
