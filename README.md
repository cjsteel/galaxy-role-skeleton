## galaxy-role-skeleton

## Description

galaxy-role-skeleton is used to quickly create new ansible roles.

## Requirements

- **ansible-galaxy** command
- Python

## Usage

#### Role Names

##### Roles long name

Used as the roles repository name in cases where you have a single role per repository.

```shell
ansible-role-myrole
```

##### Roles short name

Used when creating a new role using this project.:

```shell
myrole
```

### Setup

#### Clone project fork

Clone your customised personal or business fork to your Ansible projects directory

```shell
mkdir ~/projects
cd ~/projects
git clone git@github.com:cjsteel/galaxy-role-skeleton.git
```

#### Create your role

##### Syntax example

```shell
ansible-galaxy init --role-skeleton=ALTERNATIVE_ROLE_SKELETON_PATH role-short-name
```

#### Real world usage examples:

##### To create a new role

```shell
mkdir -p ~/projects/your-ansible-project/roles
cd ~/projects/your-ansible-project/roles
ansible-galaxy init --role-skeleton=~/projects/galaxy-role-skeleton/skeleton role-short-name -vvv
```

##### To overwrite an existing role

```shell
cd ~/projects/your-ansible-project/roles
ansible-galaxy init --role-skeleton=~/projects/galaxy-role-skeleton/skeleton -f existing-role-short-name -vvv
```

##### Set up your default Molecule scenario

```shell
molecule init scenario -s default -d lxd -r role-short-name
```

## Troubleshooting

### Molecule

#### pytest bug: Fix for error"AttributeError: 'Config' object has no attribute 'cache'

* [Possible bug with the 3.10.0 release #4304](https://github.com/pytest-dev/pytest/issues/4304)

```shell
touch molecule/default/pytest.ini" like this one.
```

```ini
[pytest]
addopts = -p no:cacheprovider -p no:stepwise
```

## Author(s) and license

- [Christopher Steel](http://mcin-cnim.ca/) | [e-mail](mailto:christopher.steel@mcgill.ca)

License: [MIT](https://tldrlegal.com/license/mit-license)

