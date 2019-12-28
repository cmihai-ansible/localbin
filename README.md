Role Name
=========

localbin: download, unpack and install various tools to /usr/local/bin or a defined
directory. Example: install pandoc.

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

```yaml
localbin_user: root
localbin_dir: "/usr/local/bin"
localbin_tools:
  - name: hugo
    url: "https://github.com/gohugoio/hugo/releases/download/v0.58.3/hugo_0.58.3_Linux-64bit.tar.gz"
    version: "0.58.3"
    version_command: "version"
    checksum: "sha256:92aeeb64d4c392782cb55424dc2cc594a06ad5e1bc7e156480feab488ff7e774"
    extra_opts: ["--wildcards", "hugo"]
  - name: micro
    url: "https://github.com/zyedidia/micro/releases/download/nightly/micro-2.0.0-rc1.dev.24-linux64.tar.gz"
    version: "2.0.0-rc1.24"
    version_command: "--version"
    checksum: "sha256:a4104bacbe1c39708339501e28fa8f74fb64076e4a133edd039a8d9c1fcd124d"
    extra_opts: ["--strip=1", "--wildcards", "*/micro"]
  - name: pandoc
    version: "2.9.1"
    version_command: "--version"
    url: "https://github.com/jgm/pandoc/releases/download/2.9.1/pandoc-2.9.1-linux-amd64.tar.gz"
    checksum: "sha256:1a2f66ffa66d3fa82cd1cdba3fe6e094562f9513f44a0f587ed7d51af413880b"
    extra_opts: ["--strip=2", "--wildcards", "*/pandoc*"]
  - name: scc
    version: "2.10.1"
    version_command: "--version"
    url: "https://github.com/boyter/scc/releases/download/v2.10.1/scc-2.10.1-x86_64-unknown-linux.zip"
    checksum: "sha256:663da4a750fd4f0f3d9328dd58f6850c46f458f94258c04b78b630e47d667ff8"
  - name: shellcheck
    version: "0.7.0"
    version_command: "--version"
    url: "https://storage.googleapis.com/shellcheck/shellcheck-stable.linux.x86_64.tar.xz"
    checksum: "sha256:092f8ece0bb8413c835f4ecc14c9f1157ebb44a36a216e3d617d1048ecdfce1b"
    extra_opts: ["--strip=1", "--wildcards", "*/shellcheck"]
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
