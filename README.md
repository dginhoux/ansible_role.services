Ansible Role : dginhoux.services
=========

This ansible role configure services state. t support sysvinit and systemd.


Requirements
------------

This role require a supported platform defined in `meta/main.yml`.
It will skip node with unsupported platform ; this behaviour can be bypassed by settings this variable `asserts_bypass=True`.



Role Variables
--------------

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


Dependencies
------------

none


Example Playbook
----------------



License
-------

BSD


Author Information
------------------

https://github.com/dginhoux/
