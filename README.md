# ROLE dginhoux.services



## DESCRIPTION

This ansible role configure services state.<br />
It support sysvinit and systemd.



## REQUIREMENTS

#### SUPPORTED PLATFORMS

This role require a supported platform.<br />
It will skip node with unsupported platform to avoid any compatibility problem.<br />
This behaviour can be bypassed by settings the following variable `asserts_bypass=True`.

| Platform | Versions |
|----------|----------|
| Debian | buster, bullseye |
| Fedora | 33, 34, 35, 36 |
| EL | 7, 8 |

#### ANSIBLE VERSION

Ansible >= 2.12

#### DEPENDENCIES

None.



## INSTALLATION

#### ANSIBLE GALAXY

```shell
ansible-galaxy install dginhoux.services
```
#### GIT

```shell
git clone https://github.com/dginhoux/ansible_role.services dginhoux.services
```


## USAGE

#### EXAMPLE PLAYBOOK

```yaml
- hosts: all
  roles:
    - name: start role dginhoux.services
      ansible.builtin.include_role:
        name: dginhoux.services
```


## VARIABLES

#### DEFAULT VARIABLES

Defaults variables defined in `defaults/main.yml` : 

```yaml
services_list:
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
```

#### DEFAULT OS SPECIFIC VARIABLES

Those variables files are located in `vars/*.yml` are used to handle OS differences.<br />
One of theses is loaded dynamically during role runtime using the `include_vars` module and set OS specifics variable's.

`NOT USED BY THIS ROLE`



## AUTHOR

Dany GINHOUX - https://github.com/dginhoux



## LICENSE

MIT
