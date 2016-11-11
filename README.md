# kubernetes-setup

## Description
This Ansible project will install a kubernetes master and some minions.


### Roles
* [kubebase](roles/kubebase) -> Install docker and kubernetes
* [kubemaster](roles/kubemaster) -> Install a kubernetes master
* [kubeminion](roles/kubeminion) -> Install a minion

### Playbooks
* [python.yml](playbooks/python.yml) -> Install python via raw module
* [master.yml](playbooks/master.yml) -> Install the kubernetes master
* [minion.yml](playbooks/minion.yml) -> Install all minions
* [setup.yml](playbooks/setup.yml) -> Install the whole kubernetes infrastructure


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

## Installation
```
# example with cluster1 inventory file
ansible-playbook -i inventories/cluster1 playbooks/setup.yml
```


## Hints
* some Ansible tasks are marked with `changed_when: false`. I know, it's not the best solution :-)


## Author
* Pascal Stauffer