# Ansible

Playbooks for setting up and maintaining Debian/Ubuntu servers.

Run all commands from the repo root.

## Setup

Install dependencies:

```bash
ansible-galaxy collection install -r requirements.yml
```

Add the server to `linux_server/inventory.ini`:

```ini
[servers]
myserver ansible_host=10.0.50.154
```

## Bootstrap

Only needed on fresh installs without sudo. Requires the root password.

```bash
ansible-playbook -i linux_server/inventory.ini linux_server/bootstrap.yml \
  --limit myserver -u USER --ask-pass --ask-become-pass
```

## Hardening

Installs packages, sets up admin SSH access, UFW, Fail2ban, and automatic updates.

```bash
ansible-playbook -i linux_server/inventory.ini linux_server/hardening.yml \
  --limit myserver -u USER --ask-pass --ask-become-pass
```

Take a VM snapshot first. Password SSH login is disabled after hardening.

## Maintenance

Check server status:

```bash
ansible-playbook -i linux_server/inventory.ini linux_server/maintenance.yml
```

Install updates:

```bash
ansible-playbook -i linux_server/inventory.ini linux_server/maintenance.yml \
  -e "apply_updates=true"
```

## Order

Bootstrap (if needed) → Hardening → Maintenance
