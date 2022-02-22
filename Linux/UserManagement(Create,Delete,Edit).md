# User Management

In linux there are three types of users:

1. Super or Root user:
   - root user is the most powerful user.
   - root is the administrator user.
2. System user:
   - user created by the softwares or applications.
3. Normal user:
   - user created by the root user.

| Type | Example | Home Directory | Shell |
| :---- | :------ | :------------- | :---- |
| super user | root | /root | /bin/bash |
| system user | ftp, ssh, apache | /var/ftp, /etc | /sbin/nologin |
| normal user | visitor, ec2-user | /home/username | /bin/bash |

All the users related information is stored in the file ```/etc/passwd```. (Lists the users)

And all the group related information is stored in the file ```/etc/group```.

## User Creation

Whenever a user is created in linux, below things will happen by default.

- A home directory is created (/home/username).
- A unique userid (uid) and groupid (gid) are given to the user.
- An entry is created in "/etc/passwd".

The syntax for creating a user in linux is:

```sh
useradd <option> <username>
```

Options are:

- u - user_id
- G - secondary group_id
- g - primary group_id
- d - home directory
- c - comment
- s - shell

```sh
useradd <USER_NAME>
passwd <USER_NAME>
```

Output:

```text
Changing password for user admin.
New password: <USER_PASSWORD>
Retype new password: <USER_PASSWORD>
passwd: all authentication tokens updated successfully.
```

## To list Users

```sh
cat /etc/passwd
```

In "/etc/passwd" user information will be shown as

>john:x:1001:/home/john:/bin/bash

In "/etc/passwd" group information will be shown as

>john:x:1001

## To delete a user

login as root and enter below command:

```sh
userdel <USER_NAME>
```

## Changing user attributes or user configuration

Adding a user to another group

```sh
usermod <option> <dest_group> <username>
```

Example:
>usermod -G john mark

## Login as another user

To login as another user you should setup password for that user.
To create password for that user execute command ```passwd <username>```

|To switch to the another user execute below command

```sh
sudo su - <user_name>
```
