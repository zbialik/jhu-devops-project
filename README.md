# jhu-devops-project

## Infrastructure Setup

1 AWS EC2 instances:
- `r5.large` 

## Tools

1. Gitlab
1. Sonarqube
1. Jenkins w/Snyk CLI

## Ansible Documentation

We have 2 playbooks, `main.yml` and `init-server.yml`:
- `init-server.yml` is ran once to update/install OS packages, including docker.
- `main.yml` is used to install/update all of our DevOps tools on the OS.

We organized `main.yml` to rely on ansible roles for each discrete tool we deploy (other than gitlab + sonarqube, which the project required deployment of in a single docker-compose file). Additionally, there is a `host-confs` role that we use to setup any pre-requisite items, such as an `/etc/hosts` file. 

The remaining 3 roles are described below:
1. [gitlab-sonarqube](./ansible/roles/gitlab-sonarqube/tasks/main.yml): deploys gitlab, sonarqube, and sonarqube's db using docker-compose (see [manifest here](./ansible/roles/gitlab-sonarqube/files/docker-compose.yml)).
1. [jenkins](./ansible/roles/jenkins/tasks/main.yml): deploys jenkins as a docker container using docker-compose (see [manifest here](./ansible/roles/jenkins/files/docker-compose.yml)).
1. [gitlab-runner](./ansible/roles/gitlab-runner/tasks/main.yml): deploys gitlab-runner as a systemd service using APT package manager.

## Ansible Usage

### Update OS Packages on Host

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

