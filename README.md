LXC-based cluster host
======================

Install and configure lxc for creating cluster based on ubuntu trusty

Role Variables
--------------

```yaml
# Basic settings for lxc networking
lxc_domain_name: lxc
lxc_ip_address: 10.0.3.1

# containers to be used as a template
lxc_containers:
 - name: ubuntu.trusty
   template: ubuntu
   release: trusty
   user: dev
   password: dev

# actual working containers, created as a cheap clones with overlayed fs
lxc_clones:
  - name: sample
    template: ubuntu.trusty
    ip: 10.0.3.22

# Expose ports from containers
lxc_forwarded_ports: []
  - source: 80
    target: 10.0.3.22:80
```

Example Playbook
----------------

```yaml
- name: LXC test playbook
  hosts: all
  vars:
    lxc_clones:
      - name: sample
        template: ubuntu.trusty
        ip: 10.0.3.3
    lxc_forwarded_ports:
      - source: 2022
        target: 10.0.3.3:22
  roles:
    - lxc
```

You can use Vagrantfile, shipped in vagrant dir

License
-------

MIT

Author Information
------------------

Arthur Orlov
