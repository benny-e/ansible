# Ansible h

Ansible playbooks for configuring, securing, and maintaining Debian/Ubuntu servers.

## Structure

```text
ansible/
├── ansible.cfg
├── requirements.yml
├── linux_server/
│   ├── inventory.ini
│   ├── hardening.yml
│   └── maintenance.yml
├── roles/
│   ├── common/
│   └── hardening/
└── proxmox/             # Planned
```

## Setup

Install required collections:

```bash
ansible-galaxy collection install -r requirements.yml
```

Add your servers to `linux_server/inventory.ini`.

Run all commands from the repository root.

## Hardening

```bash
ansible-playbook -i linux_server/inventory.ini linux_server/hardening.yml
```

Runs two roles:

- **Common:** Installs packages, creates an admin account, configures sudo and SSH keys, and verifies access.
- **Hardening:** Configures UFW, Fail2ban, automatic updates, and SSH security.

For a fresh server requiring password authentication:

```bash
ansible-playbook -i linux_server/inventory.ini linux_server/hardening.yml -u initialuser --ask-pass --ask-become-pass
```

The server must already permit SSH access for `initialuser`. Verify SSH access before disconnecting. UFW may block application ports unless explicitly allowed.

## Maintenance

Audit servers without applying updates:

```bash
ansible-playbook -i linux_server/inventory.ini linux_server/maintenance.yml
```

Audit and install available updates:

```bash
ansible-playbook -i linux_server/inventory.ini linux_server/maintenance.yml -e "apply_updates=true"
```

Reports system health, updates, disk usage, services, security status, and Docker containers.

## Proxmox (Planned)

`proxmox/deploy.yml` will automate VM creation using cloud-init, prompt for resources and networking, and apply the existing Ansible roles.
