# Ansible amtega.aide role

This is an [Ansible](http://www.ansible.com) role to setup AIDE (Advanced Intrusion Detection Environment)

## Role Variables

A list of all the default variables for this role is available in `defaults/main.yml`.

## Usage

This is an example playbook:

```yaml
---

- hosts: all
  roles:
    - role: amtega.aide
      vars:
        aide_custom_rules:
          - name: FIPSR
            pattern: 'p+i+n+u+g+s+m+c+acl+selinux+xattrs+sha256'
          - name: ALLXTRAHASHES
            pattern: 'sha1+rmd160+sha256+sha512+tiger'
          - name: EVERYTHING
            pattern: 'R+ALLXTRAHASHES'
          - name: NORMAL
            pattern: sha256
          - name: DIR
            pattern: 'p+i+n+u+g+acl+selinux+xattrs'
          - name: PERMS
            pattern: 'p+u+g+acl+selinux+xattrs'
          - name: STATIC
            pattern: 'p+u+g+acl+selinux+xattrs+i+n+b+c+ftype'
          - name: LOG
            pattern: 'p+u+g+n+acl+selinux+ftype'
          - name: CONTENT
            pattern: 'sha256+ftype'
          - name: CONTENT_EX
            pattern: 'sha256+ftype+p+u+g+n+acl+selinux+xattrs'
          - name: DATAONLY
            pattern: 'p+n+u+g+s+acl+selinux+xattrs+sha256'
        aide_acls:
          - regexp: '/boot/'
            rule: CONTENT_EX
          - regexp: '/bin/'
            rule: CONTENT_EX
          - regexp: '/sbin/'
            rule: CONTENT_EX
          - regexp: '/lib/'
            rule: CONTENT_EX
          - regexp: '/lib64/'
            rule: CONTENT_EX
          - regexp: '/opt/'
            rule: CONTENT
          - regexp: '/proc/'
            rule: 'absent'
          - regexp: '/root/\..*'
            rule: PERMS
          - regexp: '/root/'
            rule: CONTENT_EX
          - regexp: '/usr/src/'
            rule: 'absent'
          - regexp: '/usr/tmp/'
            rule: 'absent'
          - regexp: '/usr/'
            rule: CONTENT_EX
          - regexp: '/etc/'
            rule: CONTENT_EX
          - regexp: '/var/log/'
            rule: 'absent'
          - regexp: '/var/run'
            rule: 'absent'
          - regexp: '/var/'
            rule: 'CONTENT_EX'
        ```

## Testing

Tests are based on docker containers. You can setup docker engine quickly using the playbook `files/setup.yml` available in the role [amtega.docker_engine](https://galaxy.ansible.com/amtega/docker_engine).

Once you have docker, you can run the tests with the following commands:

```shell
$ cd amtega.aide/tests
$ ansible-playbook main.yml
```

## License

Copyright (C) 2020 AMTEGA - Xunta de Galicia

This role is free software: you can redistribute it and/or modify it under the terms of:

GNU General Public License version 3, or (at your option) any later version; or the European Union Public License, either Version 1.2 or – as soon they will be approved by the European Commission ­subsequent versions of the EUPL.

This role is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details or European Union Public License for more details.

## Author Information

- José Enrique Mourón Regueira
