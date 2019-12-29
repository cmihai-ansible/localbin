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

See defaults for more examples.
Will place binaries in `localbin_dir` or provided `dest`.
Will unpack .tar, .gz, .xz and .zip when setting `unpack: true`.

```yaml
localbin_user: root
localbin_dir: "/usr/local/bin"
localbin_tools:
  # Unpack, and strip leading directory path
  - name: micro
    url: "https://github.com/zyedidia/micro/releases/download/\
      v1.4.1/micro-1.4.1-linux64.tar.gz"
    checksum: "sha256:e7d4c9427f9fdfed78e69d42cf518e93ae15fc8f70b7f0f87d292ed81206e900"
    version: "1.4.1"
    version_command: "--version"
    extra_opts: ["--strip=1", "--wildcards", "*/micro"]
    unpack: true

  # Download and place in localbin_dir or provided dest
  - name: kubectl
    url: "https://storage.googleapis.com/kubernetes-release/release/\
      v1.17.0/bin/linux/amd64/kubectl"
    checksum: "sha256:6e0aaaffe5507a44ec6b1b8a0fb585285813b78cc045f8804e70a6aac9d1cb4c"
    version: "1.17"
    version_command: "version"
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
          # Unpack, and strip leading directory path
          - name: micro
            url: "https://github.com/zyedidia/micro/releases/download/\
              v1.4.1/micro-1.4.1-linux64.tar.gz"
            checksum: "sha256:e7d4c9427f9fdfed78e69d42cf518e93ae15fc8f70b7f0f87d292ed81206e900"
            version: "1.4.1"
            version_command: "--version"
            extra_opts: ["--strip=1", "--wildcards", "*/micro"]
            unpack: true

          # Download and place in localbin_dir or provided dest
          - name: kubectl
            url: "https://storage.googleapis.com/kubernetes-release/release/\
              v1.17.0/bin/linux/amd64/kubectl"
            checksum: "sha256:6e0aaaffe5507a44ec6b1b8a0fb585285813b78cc045f8804e70a6aac9d1cb4c"
            version: "1.17"
            version_command: "version"
      tags: localbin
```

License
-------

MIT

Author Information
------------------

- [Mihai Criveti](https://www.linkedin.com/in/crivetimihai/)
