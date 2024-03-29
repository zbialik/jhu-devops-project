# jhu-devops-project

## Infrastructure Setup

2 AWS EC2 instances:
- `t3.medium` for Gitlab + Sonarqube
- `TBD` for Jenkins + Snyk

### Update OS Packages on Hosts

```
cd ansible
ansible-playbook -i inventory.ini init-server.yml
```
