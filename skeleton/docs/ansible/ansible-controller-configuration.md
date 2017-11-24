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

## Recommended

We recommend installing Ansible into a virtual environment. Here we document how to do this using something called **miniconda**.

### miniconda

* [../miniconda/installing-miniconda.md](../miniconda/installing-miniconda.md)

## RecommendAnsible configuration

### list available versions

```shell
pip install yolk3k
yolk -V ansible
```

Output example

```shell
ansible 2.4.1.0
ansible 2.4.0.0
ansible 2.3.2.0
ansible 2.3.1.0
ansible 2.3.0.0
ansible 2.2.3.0	# ansible-galaxy: error: no such option: --role-skeleton
ansible 2.2.2.0	# ansible-galaxy: error: no such option: --role-skeleton
ansible 2.2.1.0 # ansible-galaxy: error: no such option: --role-skeleton
ansible 2.2.0.0 # ansible-galaxy: error: no such option: --role-skeleton
ansible 2.1.6.0
ansible 2.1.5.0
ansible 2.1.4.0
ansible 2.1.3.0
ansible 2.1.2.0
ansible 2.1.1.0
ansible 2.1.0.0
ansible 2.0.2.0
ansible 2.0.1.0
ansible 2.0.0.2
ansible 2.0.0.1
ansible 1.9.6
ansible 1.9.5
ansible 1.9.4
```

Make a note of the version you want to install

### Ensure for miniconda

### Ensure for a virtual environment

Here we create a virtual environment called **ansible-2.3** that will include python2.x

```shell
conda create -y -n ansible-2.3 python=2
```

### activate the target virtual environment

```shell
source activate ansible-2.3
```

### Confirm active virtual environment

Confirm that the environment is active by verifying that the virtual environment name is prepended to your command prompt as follows:

```shell
(ansible-2.3) cjs@automa:~/projects$ 
```

Alternativly you can use the commend `which python` and confirm that the path returned is located in your target virtual environment:

```shell
/home/cjs/miniconda2/envs/ansible-2.3/bin/python
```

### Install the latest iteration of your target ansible version

If you want ansible 2.3 you probably the latest revision, 2.3.2.0. The following will install ansible as well as any dependancies.

```shell
pip install 'ansible==2.3.2.0' 
```

Installation confirmation

```shell
which ansible
```

Output example

```shell
/home/cjs/miniconda2/envs/ansible-2.3/bin/ansible
```

Version confirmation

```shell
ansible --version
```

Output example

```shell
ansible 2.3.2.0
  config file = 
  configured module search path = Default w/o overrides
```

That's it...

