# ansible-role-pxeserver

An Ansible role for setting up and running a PXE boot server.  
Defaults can be found in the `defaults/main.yml` file.  

## Sample playbook

```yaml
---
- name: Setup and run PXE boot server
  hosts: pxeserver
  become: true

  roles:
    - role: chrisvanmeer.pxeserver
      vars:
        pxeserver_config_images:
          - label: RedHat 8.7
            kernel: redhat8/vmlinuz
            append:
              initrd: redhat8/initrd.img
              stage2: http://reposerver/deploy/repos/redhat/8/os/x86_64
              quiet: true
              ifnames: 0
              biosdevname: 0
              kickstart: http://reposerver/deploy/kickstart/redhat_8_7.cfg
          - label: Debian 11
            kernel: debian11/vmlinuz
            append:
              initrd: debian/initrd.img
              stage2: http://reposerver/deploy/repos/debian/11/os/x86_64
              quiet: true
              ifnames: 0
              biosdevname: 0
              kickstart: http://reposerver/deploy/kickstart/debian_11.cfg
          - label: DBAN
            kernel: dban/vmlinuz
            append:
              initrd: dban/initrd.img
          - label: Local disk
            default: true
            localboot: true
```
