# ROLE dginhoux.services_state

## DESCRIPTION

This ansible role configure services state.<br />
It support sysvinit and systemd.

## REQUIREMENTS

#### SUPPORTED PLATFORMS

| Platform | Versions |
|----------|----------|
| Debian | all |
| EL | all |
| Fedora | all |
| Ubuntu | all |

#### ANSIBLE VERSION

Ansible >= 2.13

#### DEPENDENCIES

None.

## INSTALLATION

#### ANSIBLE GALAXY

```shell
ansible-galaxy install dginhoux.services_state
```
#### GIT

```shell
git clone https://github.com/dginhoux/ansible_role.services_state dginhoux.services_state
```

## USAGE

#### EXAMPLE PLAYBOOK

```yaml
- name: Playbook
  hosts: all
  roles:
    - name: Start role dginhoux.services_state
      ansible.builtin.include_role:
        name: dginhoux.services_state
```

## VARIABLES

#### DEFAULT VARIABLES

Defaults variables defined in `defaults/main.yml`

#### EXAMPLES VARIABLES

```yaml
services_state_list:
  - enabled: true
    state: restarted
    systemd:
      name: keepalived.service
      # masked: false
      # scope: system
    sysvinit:
      name: keepalived
      runlevel: 3

  - enabled: true
    state: restarted
    systemd:
      name: rsyslog.service
      masked: false
      scope: system
    sysvinit:
      name: rsyslog
      # runlevel: 3

  - enabled: true
    state: stopped
    systemd:
      name: "{{ 'httpd.service' if ansible_os_family == 'RedHat' else 'apache2.service' }}"
      # masked: false
      # scope: system
    sysvinit:
      name: "{{ 'httpd' if ansible_os_family == 'RedHat' else 'apache2' }}"
      runlevel: 3

services_state_list_group: []
services_state_list_host: []
```

NOTE : Theses 3 lists `services_state_list`, `services_state_list_group` and `services_state_list_host` are merged. <br />
You can use the `_host` and `_group` lists to specify per host and/or per group content.


#### DEFAULT OS SPECIFIC VARIABLES

Those variables files are located in `vars/*.yml` are used to handle OS differences.<br />
One of theses is loaded dynamically during role runtime using the `include_vars` module and set OS specifics variable's.

`NOT USED BY THIS ROLE`

## AUTHOR

Dany GINHOUX - https://github.com/dginhoux

## LICENSE

MIT
