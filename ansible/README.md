Role Name
=========
https://github.com/lablabs/ansible-role-rke2.git

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

```
---
# The node type - server or agent
rke2_type: server

# Deploy the control plane in HA mode
rke2_ha_mode: false

# Install and configure Keepalived on Server nodes
# Can be disabled if you are using pre-configured Load Balancer
rke2_ha_mode_keepalived: false

# Install and configure kube-vip LB and VIP for cluster
# rke2_ha_mode_keepalived needs to be false
rke2_ha_mode_kubevip: false

# Kubernetes API and RKE2 registration IP address. The default Address is the IPv4 of the Server/Master node.
# In HA mode choose a static IP which will be set as VIP in keepalived.
# Or if the keepalived is disabled, use IP address of your LB.
rke2_api_ip: "192.168.1.78"

# RKE2 version
rke2_version: v1.29.0+rke2r1

```

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```
  ---
- name: Deploy RKE2
  hosts: k8s_cluster
  become: true
  roles:
     - role: ansible-role-rke2
```
Example Command
----------------
```
ansible-playbook playbooks/deploy_rke2.yml -i inventories/hosts -u kube --ask-become-pass
```


License
-------

BSD

Author Information
------------------

Julian Doré
