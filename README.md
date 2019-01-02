## galaxy-role-skeleton

## Description

galaxy-role-skeleton is used to create new ansible galaxy compatible roles quickly. Once created you can customize them before testing.

## Updates

* Additional Customization is done by modifying files and/or [Jinja2](http://jinja.pocoo.org/) templates found in the `skeleton` directory.

## Requirements

- **ansible-galaxy** command
- Python

## Variables

The generated roles short name variable is used in the jinja2 templates and will be replaced with the roles short name wherever you specify it in jinja2 templates in the skeleton directory.

Below is the content of the  `skeleton/tasks/main.yml.j2` Jinja2 templace which is used to create your new roles `tasks/main.yml`

```shell
--- # roles/{{ role_name }}/tasks/main.yml

- name: Load OS specific variables
  include_vars: "{{ '{{' }} fact_role_path {{ '}}' }}/vars/{{ '{{' }} ansible_os_family | lower {{ '}}' }}.yml"

- name: "Debug variable values"
  include: "{{ '{{' }} fact_role_path {{ '}}' }}/tasks/debug.yml"
  when: {{ role_name }}_debug

- name: Run any OS specific tasks
  include: "{{ '{{' }} fact_role_path {{ '}}' }}/tasks/{{ '{{' }} ansible_os_family | lower {{ '}}' }}.yml"

```

On the first line `{{ role_name }}` would get replaced with your roles short name.

On the fourth line and other lines that, however, effectivly escapes the brace pairs `{{ }}.`

The templated results for a role called `ants`would look like this:

```shell
--- # roles/ants/tasks/main.yml

- name: Load any OS specific variables
  include_vars: "{{ fact_role_path }}/vars/{{ ansible_os_family | lower }}.yml"

- name: "Debug variable values"
  include: "{{ fact_role_path }}/tasks/debug.yml"
  when: ants_debug

- name: Run any OS specific tasks
  include: "{{ fact_role_path }}/tasks/{{ ansible_os_family | lower }}.yml"
```

#### Role Name

##### Roles long name

Used as the roles repository name in cases where you have a single role per repository.

```shell
ansible-role-fetch
```

##### Roles short name

Name used when cloning a single role repository locally. The *short name* for our role in this example is:

```shell
fetch
```

## Usage

### Usage as an alternative to the default ansible-galaxy role skeleton

Syntax example:

```shell
ansible-galaxy init --role-skeleton=ALTERNATIVE_ROLE_SKELETON_PATH new_role_short_name
```

### Usage example

Generateding a role called test. Note that the -f will force any existing role to be overwritten:

```shell
cd ~/projects/ansible/roles
ansible-galaxy init --role-skeleton=~/projects/galaxy-role-skeleton/skeleton -f testrole -vvv
```

Initialize new role for Molecule

```shell
molecule init scenario -s default -d lxd -r testrole
```

#### pytest bug: Fix for error"AttributeError: 'Config' object has no attribute 'cache'

* [Possible bug with the 3.10.0 release #4304](https://github.com/pytest-dev/pytest/issues/4304)

```shell
touch molecule/default/pytest.ini" like this one.
```

```ini
[pytest]
addopts = -p no:cacheprovider -p no:stepwise
```

### Authors and license

- [Christopher Steel](http://mcin-cnim.ca/) | [e-mail](mailto:christopher.steel@mcgill.ca)

License: [MIT](https://tldrlegal.com/license/mit-license)

