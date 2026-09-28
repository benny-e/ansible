Ansible playbook for quickly configuring a hardened linux debian server.

Includes SSH key setup/hardening, UFW, fail2ban, common tools, and unattended upgrades.

Usage:
```
ansible-playbook -i 'SERVER_IP,' -u USER -k -K harden.yml
```

Setting custom admin user:
```
ansible-playbook -i 'SERVER_IP,' -u USER -k -K -e admin_user=myuser harden.yml
```
