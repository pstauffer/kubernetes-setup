# kubernetes-setup

[![Build Status](https://travis-ci.org/pstauffer/kubernetes-setup.png?branch=master)](https://travis-ci.org/pstauffer/kubernetes-setup)


## Description
This Ansible project will install a kubernetes master and some minions, based on the [getting started Guide](http://kubernetes.io/docs/getting-started-guides/kubeadm/).
The installation has been tested on the **[Ubuntu 16.04 LTS - Xenial (HVM)](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)** and **[CentOS 7 (x86_64) - with Updates HVM](https://aws.amazon.com/marketplace/pp/B00O7WM7QW)** image in the [AWS Cloud](https://aws.amazon.com). The packages are tagged with fix versions, which are working with this Ansible playbooks. The defined versions can be found in the [kubebase defaults](roles/kubebase/defaults/main.yml).

### Roles
* [kubebase](roles/kubebase) -> Install docker and kubernetes
* [kubemaster](roles/kubemaster) -> Install a kubernetes master
* [kubeminion](roles/kubeminion) -> Install a minion

### Playbooks
* [python_ubuntu.yml](playbooks/python_ubuntu.yml) -> Install python on ubuntu via raw module
* [python_centos.yml](playbooks/python_centos.yml) -> Install python on centos via raw module
* [master.yml](playbooks/master.yml) -> Install the kubernetes master
* [minion.yml](playbooks/minion.yml) -> Install all minions
* [setup.yml](playbooks/setup.yml) -> Install the whole kubernetes infrastructure


## Requirements
* Ansible 2.x
* Ubuntu 16.04 or CentOS 7.x

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

### Edit the new inventory file
* define the master and minion ip addresses 
* define your own kubemaster_token (Hint: [Ansible Vault](http://docs.ansible.com/ansible/playbooks_vault.html))
* *set the private_key_file path* (optional)
* *set the remote user* (optional)
* *set the python decision* (optional)

```
[cluster:vars]

# kubernetes part
kubemaster_token = abcdef.abcdefabcdefabcd

# ansible part
ansible_ssh_private_key_file = sshkey.pem
ansible_user = ubuntu

# python part
install_python_centos = false
install_python_ubuntu = true
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
[MIT](LICENSE)

## Author
* Pascal Stauffer