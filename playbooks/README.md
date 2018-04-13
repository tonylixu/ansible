## Ansible Playbooks

### Requirements
* Ansible v2.0+
```bash
$ ansible --version
ansible 2.4.3.0
```

### Available Playbooks
* aws-docker
  * You will have to have an running EC2 instance before you can run the `docker` playbook.
  * Update the `hosts` file
  * Run the following command:
```bash
ansible-playbook --private-key=~/.ssh/your-aws-private-key.pem --become --user=ec2-user --inventory-file=hosts main.yml --tags "aws-docker" -vvv
```
