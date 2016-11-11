# kubernetes-setup

## Description
This Ansible project will install a kubernetes master and some minions.
The installation has been tested on **Ubuntu 16.04** in the [AWS Cloud](https://aws.amazon.com).

### Roles
* [kubebase](roles/kubebase) -> Install docker and kubernetes
* [kubemaster](roles/kubemaster) -> Install a kubernetes master
* [kubeminion](roles/kubeminion) -> Install a minion

### Playbooks
* [python.yml](playbooks/python.yml) -> Install python via raw module
* [master.yml](playbooks/master.yml) -> Install the kubernetes master
* [minion.yml](playbooks/minion.yml) -> Install all minions
* [setup.yml](playbooks/setup.yml) -> Install the whole kubernetes infrastructure


## Requirements
* Ansible 2.x
* Ubuntu 16.04

## Configuration

### Default Project values
* the kubernetes master is also a node. See [kubemaster_and_minion Variable](roles/kubemaster/defaults/main.yml)
* you can define a list with plugins. See [kubemaster_plugins Variable](roles/kubemaster/defaults/main.yml)


### Create new inventory file
```
# switch in the inventories directory
cd inventories

# copy the sample file
cp sample cluster1
```

### Edit the new invetory file
* define the master and minion ip addresses 
* define your own kubemaster_token (Hint: [Ansible Vault](http://docs.ansible.com/ansible/playbooks_vault.html))
* *set the private_key_file path* (optional)
* *set the remote user* (optional)

```
[cluster:vars]
kubemaster_token = abcdef.abcdefabcdefabcd
ansible_ssh_private_key_file = sshkey.pem
ansible_user = ubuntu
```

## Usage
```
# example with cluster1 inventory file
ansible-playbook -i inventories/cluster1 playbooks/setup.yml
```

## Disclaimer
* works only on **Ubuntu 16.04**
* all tasks run as `root`, `become = True` is set in [ansible.cfg](ansible.cfg)
* some Ansible tasks are marked with `changed_when: false`. Sorry for that ;-)

## License
MIT

## Author
* Pascal Stauffer