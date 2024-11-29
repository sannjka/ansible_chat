# Deploy webapp with Ansible
---

## Featires:
- **login_preparation** - prepare server for further work
  - create user
  - copy public ssh key
  - prohibit root login and password authentication

- **site_deployment** - deploy website
  - set up firewall
  - install nginx
  - install docker
  - install git
  - deploy site

- **back2rootlogin** - if we need to return to root login
and password authentication

We need a folder `public_keys` within `login_preparation`. In this folder
there are keys of masterhosts.

In this example we use an app from [repo]. So to make it works we are going to 
need files `.env-docker` and `.env-postgres` described in README of the repo.

Tested for:
- Ubuntu 20.04
- Ubuntu 24.04
- CentOS Stream 9

## Installation

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Usage

### Prepare ssh key login on a server
Within `login_preparation` folder:
- add your server IP in inventory.ini
- add root pass for your sever in
`login_preparation/host_vars/your_server_alias`
- run playbook `playbook_user.yaml`
>```bash
># --ask-vault-pass for password in ansible vault
>ansible-playbook playbook_user.yaml --ask-vault-pass
>```
> To create vaulted pass:
>```bash
>echo 'your pass' | ansible-vault encrypt_string
>```

### Deploy site
Within `site_deployment` folder:
- add your server IP in inventory.ini
- run playbook `playbook_deploy.yaml`
>```bash
>ansible-playbook playbook_deploy.yaml
>```


[repo]: https://github.com/sannjka/chat.git
