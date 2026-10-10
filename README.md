# Ansible Rescript

This role deploys [rescript](https://gitlab.com/sulfuror/rescript.sh), a Bash wrapper for [Restic](https://github.com/restic/restic).

## Dependencies

- Restic
- Ansible Vault for secrets

## Installation

Install from Ansible Galaxy:

```bash
ansible-galaxy role install sebastian13.rescript -p roles
```

Or clone it locally:

```bash
git clone https://github.com/sebastian13/ansible-rescript.git roles/rescript
```

## Example Playbook

```yaml
---
- name: Deploy restic and rescript
  hosts: restic_servers
  become: true

  roles:
    - role: sebastian13.restic
    - role: sebastian13.rescript

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

Sensitive values such as passwords and secret keys should be encrypted with Ansible Vault:

```bash
ansible-vault encrypt_string --stdin-name 'RESTIC_PASSWORD'
```

Then run the playbook with vault access enabled:

```bash
ansible-playbook rescript.yml --ask-vault-pass
```

## Resources

- [sulfuror/rescript.sh](https://gitlab.com/sulfuror/rescript.sh)
- [restic/restic](https://github.com/restic/restic)
- [restic.net](https://restic.net/)
- [ansible-restic](https://github.com/sebastian13/ansible-restic)
