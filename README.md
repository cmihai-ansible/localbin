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

See defaults for more examples. Can download and unpack .tar, .gz, .xz and .zip.
Can also install binaries by making them executable. See the `copy: true` option.

```yaml
localbin_user: root
localbin_dir: "/usr/local/bin"
localbin_tools:
  - name: pandoc
    version: "2.9.1"
    version_command: "--version"
    url: "https://github.com/jgm/pandoc/releases/download/2.9.1/pandoc-2.9.1-linux-amd64.tar.gz"
    checksum: "sha256:1a2f66ffa66d3fa82cd1cdba3fe6e094562f9513f44a0f587ed7d51af413880b"
    extra_opts: ["--strip=2", "--wildcards", "*/pandoc*"]
  - name: kubectl
    url: "https://storage.googleapis.com/kubernetes-release/release/\
      v1.17.0/bin/linux/amd64/kubectl"
    checksum: "sha256:6e0aaaffe5507a44ec6b1b8a0fb585285813b78cc045f8804e70a6aac9d1cb4c"
    version: "1.17"
    version_command: "version"
    copy: true
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
        localbin_user: root
        localbin_dir: "/usr/local/bin"
        localbin_tools:
          - name: hugo
            url: "https://github.com/gohugoio/hugo/releases/download/v0.58.3/hugo_0.58.3_Linux-64bit.tar.gz"
            version: "0.58.3"
            version_command: "version"
            checksum: "sha256:92aeeb64d4c392782cb55424dc2cc594a06ad5e1bc7e156480feab488ff7e774"
            extra_opts: ["--wildcards", "hugo"]
      tags: localbin
```

License
-------

MIT

Author Information
------------------

- [Mihai Criveti](https://www.linkedin.com/in/crivetimihai/)
