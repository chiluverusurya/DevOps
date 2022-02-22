# Root Access and Enabling Password Based Login

## Grant root access to the new user by editing "/etc/sudoers" file using "visudo" command

***Note:*** Always use visudo to edit sudoers file

```bash
sudo visudo
```

Add below statements at the end of the file.

```text
<USER_NAME> ALL=(ALL:ALL) ALL
```

This means that our root user can run any command using sudo, as long as they provide their password.

1. The first field indicates the username that the rule will apply to (root).
2. The first “ALL” indicates that this rule applies to all hosts.
3. Second “ALL” indicates that the root user can run commands as all users
4. Third “ALL” indicates that the root user can run commands as all groups.
5. The last “ALL” indicates these rules apply to all commands

```bash
<USER_NAME> ALL=(ALL) NOPASSWD: ALL
```

This means that our root user can run any command using sudo, without providing their password.

## Enabling Password based login

Open the sshd_config file to enable password based login

```bash
vi /etc/ssh/sshd_config
```

* Inside the file search for the keyword `/Password` and press enter
* Change the `PasswordAuthentication no` to `PasswordAuthentication yes`
* Save and exit

Reload the file to effect the changes by executing below command.

```bash
service sshd reload
```

Now the created new user has root access (administrator priviliges) and can login using ssh with password.