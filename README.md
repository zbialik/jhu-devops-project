# jhu-devops-project

## Infrastructure Setup

2 AWS EC2 instances:
- `r5.large` for Gitlab + Sonarqube
- `TBD` for Jenkins + Snyk

### Update OS Packages on Hosts

```
cd ansible
ansible-playbook -i inventory/jhu-devops.ini init-server.yml
```

### Deploy Containers

```
cd ansible
ansible-playbook -i inventory/jhu-devops.ini main.yml
```

