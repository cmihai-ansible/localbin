Role Name
=========

localbin

[![Build Status](https://travis-ci.org/cmihai-ansible/localbin.svg?branch=master)](https://travis-ci.org/cmihai-ansible/localbin)

Ansible galaxy:
---------------

[https://galaxy.ansible.com/crivetimihai/localbin](https://galaxy.ansible.com/crivetimihai/localbin)

```bash
ansible-galaxy install crivetimihai.localbin
```

Requirements
------------

- For RHEL, a Red Hat subscription or functional local repository.

Role Variables
--------------

```
localbin_remove_packages: true
localbin_enable_service: true
localbin_enable_selinux: true
localbin_firewall_configure: true
localbin_firewall_rules:
  - service:
```

Dependencies
------------

- For Red Hat, subscription-manager.

Example Playbook
----------------

```yaml
---
- name: Install localbin on localhost
  hosts:
    - localhost
  connection: local

  tasks:
    - name: localbin is configured
      import_role:
        name: crivetimihai.localbin
      vars:
        localbin_remove_packages: true
        localbin_enable_service: true
        localbin_firewall_configure: true
        localbin_firewall_rules:
          - service:
      tags: localbin
```

License
-------

MIT

Author Information
------------------

- [Mihai Criveti](https://www.linkedin.com/in/crivetimihai/)
