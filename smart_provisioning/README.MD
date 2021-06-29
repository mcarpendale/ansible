# Pure Storage Flash Array - Smart Provisioning
This smart provisioning demo/example is based off the work Simon has done [`here`](https://github.com/PureStorage-OpenConnect/ansible-playbook-examples/tree/master/flasharray)


This playbook will
- Create a volume on the Flash Array with the `lowest` used capacity


## Requirements
### The Pure Storage FlashArray collection depends upon:
- Ansible 2.9 or later
- Pure Storage FlashArray system running Purity 4.6 or later
  - some modules require higher versions of Purity
  - some modules require specific Purity versions
- purestorage >=v1.19
- py-pure-client >=v1.14
- Python >=v2.7


## Pre-Requisites
- Update the ``vars/main.yml`` file with your relevant details
``` YAML
arrays:
  - url: 10.0.0.1
    api: 84f1db69-0000-1111-2222-33333333333d
  - url: 10.0.0.2
    api: 84f1db69-0000-1111-2222-33333333333e
  ```

## Running the demo/example
To create the demo/example volume run the following playbook:
 > `simple_sp_example.yaml`

Play will pause, waiting for `manual` intervention. Upon `continue`, volume will be *destroyed* and **eradicated**
