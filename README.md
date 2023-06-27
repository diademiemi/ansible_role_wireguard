Ansible Role Wireguard
=========

[![Molecule Test](https://github.com/diademiemi/ansible_role_wireguard/actions/workflows/molecule.yml/badge.svg)](https://github.com/diademiemi/ansible_role_wireguard/actions/workflows/molecule.yml)

Ansible role to install and configure a Wireguard network. It can generate keys or use existing ones to connect to externally configured peers.  

It will automatically use all hosts in the play as peers connecting to the given master node (`wireguard_master_inventory_hostname`). An additional list of peers can be added to the Wireguard interface with the `wireguard_additional_peers` variable.  

You can use this just to connect to an existing host by omitting the `wireguard_master_inventory_hostname` variable and just using the `wireguard_additional_peers` variable.  


Requirements
------------
These platforms are supported:
- Ubuntu 20.04  
- Ubuntu 22.04  
- Debian 10  
- Debian 11  
- EL 8 (Tested on Rocky Linux 8)  
- EL 9 (Tested on Rocky Linux 9)  
- Fedora 38  
- openSUSE Leap 15.4

Networking requirements:  
- Port 51820/UDP (or `wireguard_port`) must be accessible on the master host.  

Role Variables
--------------

| Variable | Default | Description |
|----------|---------|-------------|
| `wireguard_master_inventory_hostname` | `""` | The inventory hostname of the master node. |
| `wireguard_master_ip` | IP of master | The IP address of the master node. |
| `wireguard_port` | `51820` | The port to use for Wireguard. |
| `wireguard_interface_name` | `"wg0"` | The name of the Wireguard interface. |
| `wireguard_private_key` | `""` | The private key to use for the Wireguard interface. Will be generated if not set. |
| `wireguard_public_key` | `""` | The public key to use for the Wireguard interface. Will be inferred from private key. |
| `wireguard_ip` | `"192.168.150.1/24"` | The IP address to use for the Wireguard interface. |
| `wireguard_iptables_forward` | `true` | Whether to enable iptables forwarding. |
| `wireguard_physical_interface` | `""` | The physical interface to forward to |
| `wireguard_additional_peers` | `[]` | A list of additional peers to add to the Wireguard interface. |

Dependencies
------------
<!-- List dependencies on other roles or criteria -->
None

Example Playbook
----------------

```yaml
- name: Use diademiemi.wireguard role
  hosts: "{{ target | default('wireguard') }}"
  roles:
    - role: "diademiemi.wireguard"
      tags: ['diademiemi', 'wireguard', 'setup']
```

License
-------

MIT

Author Information
------------------

- diademiemi (@diademiemi)

Role Testing
------------

This repository comes with Molecule tests for Docker on the supported platforms.
Install Molecule by running

```bash
pip3 install -r requirements.txt
```

Run the tests with

```bash
molecule test
```
