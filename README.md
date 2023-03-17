# Wireguard
Ansible role to install and configure a Wireguard network. It can generate keys or use existing ones to connect to externally configured peers.   

It will automatically use all hosts in the play as peers connectng to the given master node. An additional list of peers can be added to the Wireguard interface with the `wireguard_additional_peers` variable.  
You can use this just to connect to an existing host by omitting the `wireguard_master_inventory_hostname` variable and using the `wireguard_additional_peers` variable.  

## Requirements
- Port 51820/UDP must be open on the master.

## Variables
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