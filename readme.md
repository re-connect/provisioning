# Provisioning

## Install requirements

```bash
ansible-galaxy install -r ./requirements.yml --force -p library
```

## Provision

```bash
ansible-playbook -i envs/pro/preprod playbook.yml --ask-vault-pass
```

Or to create the file `.vault_pass` and then fill it with the vault password

```bash
ansible-playbook -i envs/pro/preprod playbook.yml --vault-password-file=.vault_pass
```
