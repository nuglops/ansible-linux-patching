# Ansible Linux Patching from Local RHEL/OEL Repo

Automates secure and scheduled patching of Red Hat or Oracle Linux systems from a local repository, using Ansible.

## Features

- Patches systems based on dynamic host list (`servers.list`)
- Supports both full and security-only patching
- Uses a localized repo (`http://local.repo.example.com`)
- Automatic reboot after patching if required

## Usage

### 1. Generate Inventory
```bash
awk '{print $1}' servers.list > inventory.ini
echo "[linux_hosts]" | cat - inventory.ini > temp && mv temp inventory.ini
```

### 2. Run the Playbook
```bash
ansible-playbook -i inventory.ini patch.yml
```

### 3. Set Patch Mode
Modify `group_vars/all.yml`:
```yaml
patch_mode: "safe"  # or "full"
```

## Requirements

- Ansible 2.9+
- SSH key access to target hosts
- Local repo configured to serve RHEL/OEL RPMs

## License

MIT
