# ansible
Ansible playbook repo

### Hosts definition
Before you actually run a playbook, make sure you replace your user_name, also defined host in /etc/ansible/hosts

For exmaple:
[host1]
IP

### User ssh permissions
user_name should have ssh key authntication (no password) and sudo right on the target host

### To run a playbook
$ ansible-playbook main.yml -v
