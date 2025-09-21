# Nvidia role

Role to deploy Nvidia drivers on both RHEL9/Ubuntu.

## WARNING
On RHEL9, this role can update the Nvidia drivers unintentionally. This seems to be due to a bug in Ansible.
```
- name: Install NVIDIA driver and NVIDIA Docker Container Toolkit base
  ansible.builtin.dnf:
    name:
      - "@nvidia-driver:open-dkms"
      - "nvidia-container-toolkit-base"
    state: present # would be latest if I wanted to install latest, but seems to install latest anyways
  notify: Reboot system
```