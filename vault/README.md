## What is Ansible Vault
Ansible vault is a feature of Ansible that allows keeping sensitive data such as passwords or keys in encrypted files, rather than as plaintext in your playbooks or roles. These vault files can then be distributed or placed in source control.

### Enable Ansible Vault
To enable this feature, a command line tool `ansible-vault` is used to edit files, and a command line flag `--ask-vault-pass` or `--vault-password-file` is used. Alternatively, you may specify the location of a password file or command Ansible to always prompt for the password in your `ansible.cfg` file.

### What Can Be Encrypted
Basically any structured data file used by Ansible can be encrypted. For example, `group_vars` or `host_vars` inventory variables, and variables loaded by `include_vars` or `var_files`.

Ansible tasks, handlers, and so on are also data so these can be encrypted with vault as well. To hide the names of variables that you're using you can encrypt the task files as well.

The vault feature can also encrypt arbitrary files, even binary files. If a vault-encrypted file is given as the `src` argument to the `copy`, `template`, `unarchive`, `script` or `assemble` modules, the file will be placed at the destination on the target host decrypted.


### Creating Encrypted Files
To create a new encrypted data file:
```bash
$ ansible-vault create foo.yml
```
First you will be prompted for a password. The password used with vault currently must be the same for all files you wish to use together at the same time.

After providing a password, the tool will launch whatever editor you have defined with $EDITOR, and defaults to vi (before 2.1 the default was vim). Once you are done with the editor session, the file will be saved as encrypted data. The default cipher is AES.

### Editing Encrypted Files
To Edit an encrypted file in place, use the `ansible-valut edit` command. This command will decrupt the file to a temp file and allow you to edit, saving it back when done and remove the temp file:
```bash
$ ansible-vault edit foo.yml
```

### Rekeying Encrypted Files
Should you want to change your password on vault-encrypted file or files, you could:
```bash
$ ansible-vault rekey foo.yml bar.yml baz.yml
```
This command can rekey multiple data files at once and will ask for the original password and also the new password.

### Encrypting Unencrypted Files
If you have existing files that you wish to encrypt, use the `ansible-vault` encrypt command. This command can operate on multiple files at once:
```bash
$ ansible-vault encrypt foo.yml bar.yml baz.yml
```

### Decrypting Encrypted Files
If you have existing files that you no longer want to keep encrypted, you can permanently decrypt them by running the `ansible-vault decrypt` command. This command will save them unencrypted to the disk, so be sure you do not want ansible-vault edit instead:
```bash
$ ansible-vault decrypt foo.yml bar.yml baz.yml
```

### Viewing Encrypted Files
You can use `ansible-vault view` command to view encrypted files:
```bash
$ ansible-vault view foo.yml bar.yml baz.yml
```

### Use encrypt_string to create encrypted variables to embed in yaml
You can use the `ansible-vault encrypt_string` command to encrypt a string into a format that can be included in playbook YAML files.
For example:
```bash
$ ansible-vault encrypt_string --vault-id a_password_file 'foobar' --name 'the_secret'

Result:
the_secret: !vault |
      $ANSIBLE_VAULT;1.1;AES256
      62313365396662343061393464336163383764373764613633653634306231386433626436623361
      6134333665353966363534333632666535333761666131620a663537646436643839616531643561
      63396265333966386166373632626539326166353965363262633030333630313338646335303630
      3438626666666137650a353638643435666633633964366338633066623234616432373231333331
      6564
```