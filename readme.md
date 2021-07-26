# Provisioning

## Install requirements

This will install all the public roles listed in the `requirements.yml` in the library folder

```bash
ansible-galaxy install -r ./requirements.yml --force -p library
```

## Provision

This will install all the necessary middlewares needed to run a Symfony application
You will need the Ansible Vault password to get it running, ask it from a team member

To run the provisioning, launch

```bash
ansible-playbook -i envs/{website}/{environment} playbook.yml --ask-vault-pass
```

Available websites are :
* pro
* vault

Available environments are :
* preprod
* prod

Or to create the file `.vault_pass` and then fill it with the vault password

```bash
ansible-playbook -i envs/{website}/{environment} --vault-password-file=.vault_pass
```

## What is inside ?

* Git / NodeJs / Yarn / Crontab / Certbot
* Php / Composer / MySql / Nginx
* Imagick extension + Ghostscript + Imagick policy granting access to pdfs for developper
* Creates a user www-data, and copy ssh access from root to www-data
* Ssh key generation, this can be used as a deploy key
* Add gitlab.com to known hosts
* Conpatibility with certbot and nginx
