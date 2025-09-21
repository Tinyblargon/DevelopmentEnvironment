# DevelopmentEnvironment

My Development Environment

## Prerequisites

- [Mount cache disk (optional)](docs/cache_disk.md)

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
ansible-playbook -K playbook.yml
```

### Manual steps

Sadly some things can't be automated

- add the `tomoki1207.pdf` vscode extension manually.
