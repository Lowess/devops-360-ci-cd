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

### 2.1. Ansible

* Spin up the CI/CD stack using [Ansible](https://www.ansible.com/). Make sure your inventory file `ansible/inventories/vms/hosts` and your group_vars `ansible/inventories/vms/group_vars/all/libvirt/vars.yml` are configured properly.

* Run `ansible-galaxy install -r requirements.yml` in order to install role's dependencies from [Ansible Galaxy](https://galaxy.ansible.com/)

* Run the two following ansible playbooks:
```sh

cd ansible

# Setup the Drone CI CD server
ansible-playbook inventories/vms drone.yml

# Setup the Webserver running the SPA
ansible-playbook inventories/vms spa.yml
```

## 3. Stage 3 - Create the CI / CD pipeline for [DevOps-360-react] app (https://github.com/Lowess/devops-360-react) using a `.drone.yml`

http://plugins.drone.io/

http://plugins.drone.io/drone-plugins/drone-github-release/


## 4. Stage 4 - Play and understand how CI / CD pipelines enhance a development process

TODO