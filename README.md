# DevOps 360° CI / CD

DevOps 360° CI / CD is an introduction to CI/CD with [Drone](http://drone.io/), [Ansible](https://www.ansible.com/) and [ReactJS](https://reactjs.org/). For more details about the project, please check: http://slides.com/floriandambrine/devops360

## 1. Stage 1 - Design a CI / CD / CDD Workflow

* Continuous Integration (CI):

#### :round_pushpin: ................. :twisted_rightwards_arrows: ................. :twisted_rightwards_arrows: ................. :twisted_rightwards_arrows: ................. :checkered_flag:

* Continuous Delivery (CD):

#### :round_pushpin: ................. :twisted_rightwards_arrows: ................. :twisted_rightwards_arrows: ................. :twisted_rightwards_arrows: ................. :twisted_rightwards_arrows: ................. :checkered_flag:

* Continuous Deployment (CDD):

#### :round_pushpin: ................. :twisted_rightwards_arrows: ................. :twisted_rightwards_arrows: ................. :twisted_rightwards_arrows: ................. :twisted_rightwards_arrows: ................. :twisted_rightwards_arrows: ................. :checkered_flag:

## 2. Stage 2 - Setup the CI / CD Server

![CI CD Infrastructure](./docs/devops-ci-cd-infra.png "DevOps-360 CI CD Infrastructure")

### 2.1. GitHub OAuth App setup

* Follow the [Github documentation](https://developer.github.com/apps/building-oauth-apps/creating-an-oauth-app/) to setup an OAuth App

### 2.2. Ansible setup

#### 2.2.1. Drone

* Spin up the CI/CD stack using [Ansible](https://www.ansible.com/). Make sure your inventory file `ansible/inventories/vms/hosts` and your group_vars `ansible/inventories/vms/group_vars/all/libvirt/vars.yml` are configured properly.

* Run `ansible-galaxy install -r requirements.yml` in order to install role's dependencies from [Ansible Galaxy](https://galaxy.ansible.com/)

* Create a group_vars override in `ansible/inventories/vms/group_vars/drone/drone/vars.yml` to point the automation to your own [DevOps-360-react app](https://

```
drone_oauth_client: <GitHub OAuth Client>
drone_oauth_secret: <GitHub OAuth Scret>
drone_host: tp1XX.ccm.u13.org
drone_admins:
  - <Github Username 1>
  - <Github Username 2>
```

* Run the following ansible playbook to setup Drone:

```sh

cd ansible

# Setup the Drone CI CD server
ansible-playbook inventories/vms drone.yml
```

#### 2.2.2. Webserver SPA

* Fork the [DevOps-360-react app](https://github.com/Lowess/devops-360-react) project

* Create a group_vars override in `ansible/inventories/vms/group_vars/web/spa/vars.yml` to point the automation to your own [DevOps-360-react app](https://github.com/Lowess/devops-360-react) fork

```
# Setup the Webserver running the SPA
ansible-playbook inventories/vms spa.yml
```


## 3. Stage 3 - Create the CI / CD pipeline for [DevOps-360-react app](https://github.com/Lowess/devops-360-react) using a `.drone.yml`

* Create a `.drone.yml` file under the root of the [DevOps-360-react app](https://github.com/Lowess/devops-360-react)
http://plugins.drone.io/

http://plugins.drone.io/drone-plugins/drone-github-release/


## 4. Stage 4 - Play and understand how CI / CD pipelines enhance a development process

TODO