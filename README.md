# Ansible Rescript

This role deploys [rescript](https://gitlab.com/sulfuror/rescript.sh), a bash shell wrapper for [Restic](https://github.com/restic/restic).

## Dependencies

- Restic

## Example Playbook

```yaml
---

- name: Restic
  hosts: restic_servers
  become: true

  roles:
    - sebastian13.restic
    - sebsatian13.rescript
```

## Ressources

- [sulfuror/rescript.sh](https://gitlab.com/sulfuror/rescript.sh)
- [restic/restic](https://github.com/restic/restic)
- [restic.net](https://restic.net/)
- [ansible-restic](https://github.com/sebastian13/ansible-restic)