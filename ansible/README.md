# Playbooks Overview

### 1. vm-create.yml

> Create all the VMs used for the infrastructure.

```
ansible-playbook -i inventories/vms vm-create.yml
```

### 2. vm-delete.yml

> Delete all the VMs used for the infrastructure.

```
ansible-playbook -i inventories/vms vm-delete.yml
```

### 3. drone.yml

> Configure the Drone CI CD server.

```
ansible-playbook -i inventories/vms drone.yml
```

### 4. spa.yml

> Configure and install the SPA runing behind Nginx.

```
ansible-playbook -i inventories/vms spa.yml
```

### 4. deploy.yml

> Deploy the SPA runing behind Nginx.

```
ansible-playbook -i inventories/vms deploy.yml
```
