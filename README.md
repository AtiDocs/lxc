LXC-based cluster host
======================

Install and configure lxc for creating cluster based on ubuntu trusty

Role Variables
--------------

```yaml
# Basic settings for lxc networking
lxc_domain_name: lxc
lxc_ip_address: 10.0.3.1
lxc_netmask: 255.255.0.0
lxc_network: 10.10.0.0/16
lxc_dhcp_range: 10.10.255.0,10.10.255.254
lxc_dhcp_max: 253

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
    ip: 10.10.3.22

# Expose ports from containers
lxc_forwarded_ports:
  - source: 80
    target: 10.10.3.22:80
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
