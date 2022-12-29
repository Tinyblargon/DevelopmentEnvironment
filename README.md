# DevelopmentEnvironment
My Development Environment

# Install ansible

```bash
cd DevelopmentEnvironment
cp secrets.yml.example secrets.yml --no-clobber
```
populate secrets in secrets.yml
```bash
ansible-galaxy install juju4.golang
ansible-galaxy install geerlingguy.docker
ansible-playbook -K main.yml
```