# ClamAV Install and Update Role

This Ansible role installs and updates ClamAV, a popular open-source antivirus engine for  systems. It also configures ClamAV, installs necessary packages, and sets up relevant configurations.

## Requirements
- Clamav installation on a supported Linux distribution (CentOS 8 、RHEL 8 、Oracle Linux 8 or higher )

- A system with root privileges (requires root password or `sudo` access).
  You can use the following example in your playbook to run it using the `ask-pass` and `ask-become-pass` options:
  
- The `ruser` variable is the remote execution user.

```yaml
---
- name: ClamAV Install and Update
  hosts: all
  gather_facts: no
  become: true
  remote_user: "{{ ruser }}"
  become_user: root
  become_method: su
  roles:
    - clamav
...

## Role Overview

This role performs the following actions:

1. **Check EPEL repository** (if not installed):
   - Check if the EPEL repository is available.
   - Output a message if the repository is already installed.
   - Install the repository if it is not already installed.

2. **Ensure ClamAV-related packages are installed and up-to-date**:
   - Verify if the `clamav`, `clamav-update`, and `clamd` packages are installed using DNF.
   - Output a message if the packages are already installed and up-to-date.
   - Output a message if the packages are outdated or not installed.

3. **Use systemd to start and enable `clamd@scan.service`**:
   - Ensure the `clamd@scan.service` is started and enabled.
   - Verify that ClamAV updates its virus pattern definitions.
