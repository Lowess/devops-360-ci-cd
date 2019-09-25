# 1. Manual Setup of Drone CI / CD Server

## 1.1. Infrastructure overview

![CI CD Infrastructure](../docs/devops-ci-cd-infra.png "DevOps-360 CI CD Infrastructure")

## 1.2. GitHub OAuth App setup

* Follow the [Github documentation](https://developer.github.com/apps/building-oauth-apps/creating-an-oauth-app/) to setup an OAuth App

* You should endup with something like this: ![Github OAuth](../docs/github-oauth.png "GitHub OAuth")


# 2. Ansible setup

## 2.1. Drone

* Spin up the CI/CD stack using [Ansible](https://www.ansible.com/). Make sure your inventory file `ansible/inventories/vms/hosts` and your group_vars `ansible/inventories/vms/group_vars/all/libvirt/vars.yml` are configured properly.

* Run `ansible-galaxy install -r requirements.yml` in order to install role's dependencies from [Ansible Galaxy](https://galaxy.ansible.com/)

* Create a group_vars override in `ansible/inventories/vms/group_vars/drone/drone/vars.yml` to override multiple Drone settings:

> :point_up: Note that sensible data should be encrypted using `ansible-vault`. A good practice is to create a `ansible/inventories/vms/group_vars/drone/drone/vault.yml` file along side with your `vars.yml` files:

```yml
---
# vars.yml

drone_host: tp110.ccm.u13.org
drone_admins:
  - Lowess

# Secrets stored in vault.yml
drone_oauth_client: "{{ vault_drone_oauth_client }}"
drone_oauth_secret: "{{ vault_drone_oauth_secret }}"
```


```yml
---
# vault.yml

vault_drone_oauth_client: <GitHub OAuth Client>
vault_drone_oauth_secret: <GitHub OAuth Scret>
```

* Run the following ansible playbook to setup Drone (Note that if you used `ansible-vault` to encrypt secrets you will need to add `--vault-password-file <path-to-vault-file>` to your command):

```sh

cd ansible

# Setup the Drone CI CD server
ansible-playbook -i inventories/vms drone.yml
```

## 2.2. Webserver SPA

* Fork the [DevOps-360-react app](https://github.com/Lowess/devops-360-react) project

* Create a group_vars override in `ansible/inventories/vms/group_vars/web/spa/vars.yml` to point the automation to your own [DevOps-360-react app](https://github.com/Lowess/devops-360-react) fork

```
# Setup the Webserver running the SPA
ansible-playbook -i inventories/vms spa.yml
```

---

# 3. Playbooks Overview

## 3.1. `vm-create.yml`

> Create all the VMs used for the infrastructure.

```
ansible-playbook -i inventories/vms vm-create.yml
```

## 3.2. `vm-delete.yml`

> Delete all the VMs used for the infrastructure.

```
ansible-playbook -i inventories/vms vm-delete.yml
```

## 3.3. `drone.yml`

> Configure the Drone CI CD server.

```
ansible-playbook -i inventories/vms drone.yml
```

## 3.4. `spa.yml`

> Configure and install the SPA runing behind Nginx.

```
ansible-playbook -i inventories/vms spa.yml
```

## 3.5. `deploy.yml`

> Deploy the SPA runing behind Nginx.

```
ansible-playbook -i inventories/vms deploy.yml
```
