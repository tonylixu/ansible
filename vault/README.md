## What is Ansible Vault
Ansible vault is a feature of Ansible that allows keeping sensitive data such as passwords or keys in encrypted files, rather than as plaintext in your playbooks or roles. These vault files can then be distributed or placed in source control.

### Enable Ansible Vault
To enable this feature, a command line tool `ansible-vault` is used to edit files, and a command line flag `--ask-vault-pass` or `--vault-password-file` is used. Alternatively, you may specify the location of a password file or command Ansible to always prompt for the password in your `ansible.cfg` file.