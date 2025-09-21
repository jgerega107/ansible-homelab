# Homelab Collection

#### WORK IN PROGRESS!
Ansible collection used to provisioning my homelab. Some roles I've created do the following:
- Install drivers (Nvidia, ZFS) for RHEL9 and Ubuntu systems
- Install/manage Docker on RHEL9/Ubuntu systems
- Install/configure stateless observability agents (Grafana Alloy)
- Install/manage Samba
- And more

## Potential future plans
- Set up molecule (vagrant backend? need vagrant boxes representative of homelab OSes)
- Configure NFS server/mounts for clients
- Configure RKE2
- Manage Docker compose projects?
- Manage prometheus config/rulesets?
- Makefile for common operations
- Limited windows support?

## Usage

### NOTE: Inventory groups

There are certain groups and vars that these playbooks may expect. Look at the `defaults` of each role to see the var formats it expects under your host/group vars.

Some groups that the playbooks may expect

1. `nvidia`: Hosts that have a Nvidia GPU
2. `zfs`: Hosts that need ZFS drivers
3. `local`/`remote`: Hosts on local/remote networks (used for configuring Alloy push endpoints)
4. `storage`: Hosts that need to host a Samba share

### 1. Install requirements
```
# Create venv
python3 -m venv .venv

# Activate venv
. .venv bin activate

# Install python reqs (ansible)
pip install -r requirements.txt

# Install ansible reqs (collection)
ansible-galaxy install -r requirements.yml
```

### 2. Run playbook
```
ansible-playbook homelab.jgerega.docker -i yourinventoryhere.yml -K
```
