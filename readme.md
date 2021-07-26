# Provisioning

## Install requirements

This will install all the public roles listed in the `requirements.yml` in the library folder

```bash
ansible-galaxy install -r ./requirements.yml --force -p library
```

## Provision

This will install all the necessary middlewares needed to run a Symfony application
You will **need the Ansible Vault password** to get it running, ask it from a team member

To run the provisioning, create the file `.vault_pass` and then fill it with the vault password, then, run:

```bash
ansible-playbook -i envs/{website} --limit '{environment}' playbook.yml --ask-vault-pass
```

Available websites are :
* pro
* vault

Available environments are :
* preprod
* prod

```bash
ansible-playbook -i envs/{website} --limit '{environment}' --vault-password-file=.vault_pass
```

## What is inside ?

* Git / NodeJs / Yarn / Crontab / Certbot
* Php / Composer / MySql / Nginx
* Imagick extension + Ghostscript + Imagick policy granting access to pdfs for developper
* Creates a user www-data, and copy ssh access from root to www-data
* Ssh key generation, this can be used as a deploy key
* Add gitlab.com to known hosts
* Conpatibility with certbot and nginx
* Already filled dotenv files for all platforms

## First deployment

To deploy a Symfony app, you need a few things setup before, such as EasyDeployBundle, and an access to the project on gitlab

* ‼️‼️ If you plan to switch a DNS to another DNS, update its TTL to 300 at least one day before ‼️‼️
* Spawn a Debian 10 machine in the Cloud, and be sure you have SSH access as a `root` user to the machine, and get its IP address `{ip}`
* Fill its IP address in the `envs/{website}/{env}/hosts` file corresponding to `{website}` and `{env}` you want to deploy (for example `envs/pro/preprod/hosts`)
* Launch the provisioning: `ansible-playbook -i envs/{website} --limit'{environment}' --vault-password-file=.vault_pass`
* At the end of the provisioning, it should output the generated SSH key (something like `    "msg": "{ssh_key_content}"`)
* Paste this SSH key as a new item inside the `Settings/Repository/Deploy Keys` menu on gitlab
* SSH to the server as `www-data` and load it in the database running `mysql -u{db_user} {db_name} -p < ./dump.sql` and filling `{db_password}` when prompted
* You can now trigger your deployment, `cd {project_location}`, and then `symfony console deploy {environment}`

You can then test if your setup is working, and if you find no problem, you can trigger the DNS switch and SSL certificates generation

* Switch your DNS to the new IP ‼️‼️ Only do that if you TTL is really low (< 600 ), see below ‼️‼️
* Monitor your DNS switch here : [https://dnschecker.org/](https://dnschecker.org/)
* When all (or most of ) DNS are switched to the new IP, login to your server as `root` trigger SSL certificates generation `certbot --nginx`.
* When you are asked, anwser `(2) Redirect` to generate Nginx configuration to handle http->https redirection
* ‼️‼️ This setup does not include how to handle buckets, if you follow this, point to the old buckets if they exist ‼️‼️

## TODO

This section handles the things I would like to add to this repo to make it really better

* Add a role to handle generation of the `.env` file.
