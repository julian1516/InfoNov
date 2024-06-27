# Ansible Playbook for RKE2, Prometheus, and Grafana Deployment

This repository contains an Ansible playbook to automate the deployment of RKE2, Prometheus, and Grafana on a Kubernetes cluster and manifest yaml use in kubernetes. 

## Requirements

- Ansible 2.9+
- Access to the target servers
- SSH access configured for Ansible

## Variables

### Grafana Server Configuration

| Variable                | Default Value   | Description                       |
|-------------------------|-----------------|-----------------------------------|
| `grafana_security.admin_user`     | `admin`         | Grafana admin username             |
| `grafana_security.admin_password` | ``          | Grafana admin password             |
| `grafana_address`       | `192.168.1.100` | Grafana server address             |
| `grafana_alerting`      | `{}`            | Disable alerting to repair Grafana |

### Prometheus Configuration

| Variable                       | Default Value                                      | Description                                      |
|--------------------------------|----------------------------------------------------|--------------------------------------------------|
| `prometheus_ip`                | `192.168.1.100`                                    | Prometheus IP address                            |
| `prometheus_port`              | `9090`                                             | Prometheus port                                  |
| `prometheus_web_listen_address`| `192.168.1.100:9090`                               | Prometheus web listen address                    |
| `prometheus_version`           | `2.52.0`                                           | Prometheus version                               |
| `prometheus_localhost`         | `'192.168.1.100:9090'`                             | Prometheus localhost address                     |
| `prometheus_kubernetes_node`   | `'192.168.1.78:6443'`                              | Kubernetes node address for Prometheus           |
| `prometheus_config_file`       | `/home/kube/PFE_YNOV/ansible/playbooks/templates/prometheus/my_prometheus.yml.j2` | Path to Prometheus configuration file template   |
| `insecure_skip_verify`         | `true`                                             | Skip TLS verification                            |
| `kubernetes_ip`                | `192.168.1.78`                                     | Kubernetes API server IP address                 |
| `kubernetes_port`              | `6443`                                             | Kubernetes API server port                       |
| `kubernetes_api_path`          | `/api/v1/nodes/${1}/proxy/metrics/cadvisor`        | Path to Kubernetes cAdvisor metrics              |
| `bearer_token`                 | `!vault | ---`                                     | Kubernetes bearer token for authentication       |

### RKE2 Configuration

| Variable                      | Default Value                  | Description                                         |
|-------------------------------|--------------------------------|-----------------------------------------------------|
| `rke2_type`                   | `server`                       | The node type - server or agent                     |
| `rke2_ha_mode`                | `false`                        | Deploy the control plane in HA mode                 |
| `rke2_ha_mode_keepalived`     | `false`                        | Install and configure Keepalived on Server nodes    |
| `rke2_ha_mode_kubevip`        | `false`                        | Install and configure kube-vip LB and VIP for cluster|
| `rke2_api_ip`                 | `192.168.1.78`                 | Kubernetes API and RKE2 registration IP address     |
| `rke2_version`                | `v1.27.9+rke2r1`               | RKE2 version                                        |

## Usage

1. Clone the repository:

    ```sh
    https://github.com/julian1516/InfoNov.git
    cd /InfoNov
    ```

2. Update the `inventory` file with your server details.

3. Update the variables in the `group_vars` directory as needed.

4. install requirements 

5. 
Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```sh
---
- hosts: prometheus
  become: true
  roles:
    - prometheus.prometheus.prometheus
```
Example Command
----------------
```sh
ansible-playbook playbooks/deploy_prometheus.yml -i inventories/hosts -u kube --ask-vault-pass
```

## Directory Structure

```sh

├── ansible
│   ├── ansible.cfg
│   ├── inventories
│   │   ├── group_vars
│   │   │   ├── k8s_cluster.yml
│   │   │   └── supervision.yml
│   │   └── hosts
│   ├── playbooks
│   │   ├── deploy_grafana.yml
│   │   ├── deploy_prometheus.yml
│   │   ├── deploy_rke2.yml
│   │   └── templates
│   │       └── prometheus
│   │           └── my_prometheus.yml.j2
│   ├── README.md
│   └── requirements.yml
├── Manifest
│   └── kubernetes
│       ├── component.yml
│       └── supervision.yml
└── README.md
```
License
-------

BSD

Author Information
------------------

Julian Doré / Léo Gauthier / Ludovic Hubert