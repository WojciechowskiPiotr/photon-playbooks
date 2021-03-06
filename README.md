# photon-playbooks
VMware PhotonOS dedicated playbooks to automate common tasks

The playbooks are designed to run on fresh minimal PhotonOS installation.

## OS compatibility

* VMware PhotonOS 2.0
* VMware Workstation as hypervisor

## What you find in this repository

Currently available scenarios:
* Preconfigure

See details below how to use each scenario.




# Playbook: Preconfigure
This scenario is meant to run on fresh minimal PhotonOS installation. Playbook consists of 4 modules:
* Stage - on a fresh installation, it set static IP address, hostname and public SSH key authentication on the root account. Then it reboots the VM to boot it with new parameters 
* AddUser - create a local user and set public key authentication
* Packages - upgrade existing and install set of additional essential packages that are missing in the minimal installation
* Python_Docker - install from source (not the rpm) the pip, virtualenv, docker-compose and enable docker service

## Requirements
To run the playbooks, you need to ensure you fulfill following requirements:
* Fresh minimal installation of PhotonOS is made on the VM
* The VM name or IP address has to be defined in inventory in [stage] group
* The initial network configuration to fresh VM is provided via DHCP
* The final VM name have to be defined in DNS. You need to provide it in inventory [photon] group
* You need to configure root password via hypervisor console

The inventory need to contain two sections - [stage] and [photon]. The [stage] section contains a hostname or IP address assigned via DHCP to fresh PhotonOS installation. Only the playbook _playbook_stage.yml_ uses this group. The [photon] must contain the final DNS name for the VM.

Example inventory file:
```ini
[stage]
stage.mydoimain.local

[photon]
docker-vm.mydomain.local
```


## License

This project is licensed under the GNU GPL v3 license - see the [LICENSE](LICENSE) file for details