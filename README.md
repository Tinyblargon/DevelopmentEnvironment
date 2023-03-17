# DevelopmentEnvironment

My Development Environment

## Install ansible

```bash
cd DevelopmentEnvironment
```

## Populate Secrets

```bash
cp secrets.yml.example secrets.yml --no-clobber
```

## Import Ansible Roles

```bash
ansible-galaxy install --force --role-file requirements.ansible.yml
```

## Deploy

```bash
ansible-playbook -K main.yml
```
