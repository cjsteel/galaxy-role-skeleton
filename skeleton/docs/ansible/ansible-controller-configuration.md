# docs/ansible-controller-configuration.md

## Ansible Controller Requirements:

###  an unprivledged deployment user

* no root access
* no sudo access

### a very strong pass phrase

### one or more ssh keypairs

* [../ssh-keygen/generating-a-new-ssh-keypair.md](../ssh-keygen/generating-a-new-ssh-keypair.md) 

### an SSH agent

* [../ssh-agent/adding-ssh-keys-using-ssh-agent.md](../ssh-agent/adding-ssh-keys-using-ssh-agent.md)

### Ansible installation options

( see http://docs.ansible.com/ansible/latest/intro_installation.html#installation for additional methods)

#### Using the Ubuntu PPA

```
sudo apt-get update
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible
```

#### Using Conda or Miniconda

* [installing-ansible-into-a-conda-created-virtual-environment.md](installing-ansible-into-a-conda-created-virtual-environment.md)
