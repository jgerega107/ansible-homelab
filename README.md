# Homelab Collection

Work-in-progress Ansible collection for provisioning and managing a homelab.

This collection includes roles and playbooks to:

- Configure base users, packages, services, and SSH settings
- Install and manage Docker on Debian/Ubuntu systems
- Install NVIDIA and ZFS drivers
- Configure observability agents and exporters, including Grafana Alloy
- Configure Cockpit
- Install and configure Samba on the storage host

This collection is primarily tested on Debian 13.

## Potential Future Plans

- Set up Molecule testing
- Configure an NFS server and client mounts
- Configure RKE2
- Manage Docker Compose projects
- Manage Prometheus config and rules
- Add a Makefile for common operations
- Add limited Windows support
- Add support for more Linux distributions

## Inventory Expectations

The playbooks expect certain hosts or groups to exist in your inventory:

- `all`: Used by the base, Docker, observability, and Cockpit playbooks
- `cockpit`: Hosts that should receive Cockpit when running the base playbook
- `nvidia`: Hosts with an NVIDIA GPU
- `master`: Host that receives ZFS and Samba storage configuration

Role variables are documented in each role's `defaults/main.yml` and role
README.

## Install Requirements

```bash
# Create venv
python3 -m venv .venv

# Activate venv
. .venv/bin/activate

# Install Python requirements, including Ansible
pip install -r requirements.txt --upgrade

# Install Ansible collection requirements
ansible-galaxy install -r requirements.yml
```

## Run Playbooks

Run collection playbooks by their fully qualified collection name:

```bash
ansible-playbook -i yourinventoryhere.yml jgerega.homelab.base
ansible-playbook -i yourinventoryhere.yml jgerega.homelab.docker
ansible-playbook -i yourinventoryhere.yml jgerega.homelab.observability
ansible-playbook -i yourinventoryhere.yml jgerega.homelab.zfs
ansible-playbook -i yourinventoryhere.yml jgerega.homelab.nvidia
ansible-playbook -i yourinventoryhere.yml jgerega.homelab.storage
```

You can limit runs to a specific host or group:

```bash
ansible-playbook -i yourinventoryhere.yml jgerega.homelab.docker --limit appserver
```
