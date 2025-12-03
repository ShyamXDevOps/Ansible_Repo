# Ansible Deployment Project – Cache API

This repository contains an automated deployment framework built using **Ansible**.  
It is designed to deploy the **Cache API application**, manage prerequisites, and maintain consistent configurations across environments.

## 📌 Project Structure
```
Ansible/
├── ansible.cfg
├── group_vars/
│   └── all.yml
├── inventories/
│   ├── dc/
│   │   ├── hosts
│   │   └── vars.yml
│   └── tnd/
│       ├── hosts
│       └── vars.yml
├── playbooks/
│   └── cacheapi.yml
├── roles/
│   ├── prerequisite/
│   │   └── tasks/
│   │       └── main.yml
│   └── service/
│       └── tasks/
│           └── main.yml
└── shell/
   └── deploy.sh
```
## Purpose of This Project

This Ansible project automates:

- Installing required packages (e.g., rsync)
- Checking & installing **.NET 8 runtime**
- Creating deployment directory
- Copying the deployment artifact
- Handling the Cache API service restart
- Environment management using inventories (TND & DC)

It eliminates manual steps and ensures consistent deployment across multiple systems.

---

##  **Inventories**

| Environment | Path | Description |
|------------|------|-------------|
| **TND** | `inventories/tnd/hosts` | Test/Non-Production deployment hosts |
| **DC** | `inventories/dc/hosts` | Production/Data Center deployment hosts |

Each environment also contains its own `vars.yml`.

---

## **How to Run the Playbook**

### **Dry Run (Check mode)**
ansible-playbook -i inventories/tnd/hosts playbooks/cacheapi.yml --check --extra-vars "art_version=v1.0"

### **Actual Run**
ansible-playbook -i inventories/tnd/hosts playbooks/cacheapi.yml --extra-vars "art_version=v1.0"

---

## **Roles**

### **1. prerequisite**
Handles system dependencies:
- Ensures `rsync` is installed
- Checks .NET 8 runtime
- Installs .NET runtime if required

### **2. service**
Handles application deployment:
- Creates deployment directory
- Copies artifacts (`deploy.sh`, API binaries, configs)
- Restarts Cache API service (if available)

---

## Artifact Deployment

Artifacts are copied from:
shell/deploy.sh

---

## Configuration

Global variables:
group_vars/all.yml

Environment-specific variables:
inventories/tnd/vars.yml
inventories/dc/vars.yml

## 🧑‍💻 Author

**Shyam Sundar**  
DevOps & Linux Enthusiast | Ansible Automation | Cloud Learner

---

