## What is Ansible Vault
Ansible vault is a feature of Ansible that allows keeping sensitive data such as passwords or keys in encrypted files, rather than as plaintext in your playbooks or roles. These vault files can then be distributed or placed in source control.

### Enable Ansible Vault
To enable this feature, a command line tool `ansible-vault` is used to edit files, and a command line flag `--ask-vault-pass` or `--vault-password-file` is used. Alternatively, you may specify the location of a password file or command Ansible to always prompt for the password in your `ansible.cfg` file.

### What Can Be Encrypted
Basically any structured data file used by Ansible can be encrypted. For example, `group_vars` or `host_vars` inventory variables, and variables loaded by `include_vars` or `var_files`.

Ansible tasks, handlers, and so on are also data so these can be encrypted with vault as well. To hide the names of variables that you're using you can encrypt the task files as well.

The vault feature can also encrypt arbitrary files, even binary files. If a vault-encrypted file is given as the `src` argument to the `copy`, `template`, `unarchive`, `script` or `assemble` modules, the file will be placed at the destination on the target host decrypted.