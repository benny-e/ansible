# Ansible

## Harden New Server

```bash
ansible-playbook -i 'SERVER_IP,' -u USER -k -K linux_servers/harden.yml
```

Custom admin user:

```bash
ansible-playbook -i 'SERVER_IP,' -u USER -k -K -e admin_user=myuser linux_servers/harden.yml
```

## Audit Server

```bash
ansible-playbook -i inventory.ini linux_servers/maintenance.yml --limit HOST -K
```

## Audit + Update Server

```bash
ansible-playbook -i inventory.ini linux_servers/maintenance.yml --limit HOST -K -e apply_updates=true
```

## Test Connectivity

```bash
ansible all -i inventory.ini -m ping
```
