# # Pure Storage Flash Array NON Disruptive Volume Migrations demo
- Prepare Envrionment
- Migrate Volume
- Clean up

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
