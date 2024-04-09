# jhu-devops-project

## Infrastructure Setup

1 AWS EC2 instances:
- `r5.large` 

## Tools

1. Gitlab
1. Sonarqube
1. Jenkins w/Snyk

### Update OS Packages on Hosts

```bash
cd ansible
ansible-playbook -i inventory/jhu-devops.ini init-server.yml
```

### Deploy Containers

If this is the first time deploying gitlab and you don't have the gitlab-runner registration token yet, execute:

```bash
cd ansible
ansible-playbook -i inventory/jhu-devops.ini main.yml --skip-tags gitlab-runner
```

Otherwise, remaining updates can be applied like so:

```bash
cd ansible
ansible-playbook -i inventory/jhu-devops.ini -e gitlab_runner_registration_token=${TOKEN} main.yml
```
