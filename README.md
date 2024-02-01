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

  vars:
    restic_repos:
      - name: example-blocklevel-repo
        restic_repo: 's3:https://...'
        restic_password: !vault |
              $ANSIBLE_VAULT;1.1;AES256
              65616131343239383...36333833432393830
        restic_aws_id: !vault |
              $ANSIBLE_VAULT;1.1;AES256
              33326165343464663...64306164643562363
        restic_aws_key: !vault |
              $ANSIBLE_VAULT;1.1;AES256
              32356139333035363...33665666403232353
        rescript_email: "...@example.com"

    rescript_cronjobs:
      - name: example-blocklevel-backup
        repo_name: 'example-blocklevel-repo'
        cron_hour: '03'
        cron_weekday: 'MON-FRI'
```

Passwords and secret keys should be encrypted using ansible-vault

```bash
ansible-vault encrypt_string --stdin-name 'RESTIC_PASSWORD'
```

The playbook must then be run as follows:

```bash
ansible-playbook rescript.yml --ask-vault-pass
```

## Ressources

- [sulfuror/rescript.sh](https://gitlab.com/sulfuror/rescript.sh)
- [restic/restic](https://github.com/restic/restic)
- [restic.net](https://restic.net/)
- [ansible-restic](https://github.com/sebastian13/ansible-restic)