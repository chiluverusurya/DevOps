# Ansible Basics for understanding ansible

## Ansible components

* /ect/ansible/ansible.cfg => Manages ansible playbooks and commands
* Inventory/host => Stores all managed nodes ip addresses
* Tasks => Activities
* Playbook => organized/ordered collection of tasks
* Modules => Predefined commands/dependencies

## Ansible basics

* All ansible commands start with "ansible"
* Ansible default configuration file exists under /etc/ansible/ansible.cfg
* Default inventory file available uder /etc/ansible/hosts
* Managed nodes information should be available in inventory file.

## Ansible Ad-hoc commands

Ad-hoc commands are used when you dont want to repeat tasks

1. Ping:

   ```sh
   ansible all -m ping
   ```

2. Command:

   ```sh
   ansible all -m command -a "uptime"
   ```

   or

   ```sh
   ansible all -m command -a "ls -l"
   ```

   ***Note: Here -m is module and -a is argument***

3. Stat:

   Helps to know weather the target node had a particular file or not and also gives the details of the file.

   ```sh
   ansible all -m stat -a "path=/home/ansible/testfile"
   ```

4. yum:
   Helps to install packages in the target nodes.

   ```sh
   ansible all -m yum -a "name=git" -b
   ```

   Note: you need to install by becoming root so use "-b" or "-s" is used in this command

   ```sh
   ansible all -m yum -a "name=tree" -b

   ```

5. User:

   Helps to create users in target nodes

   ```sh
   ansible all -m user -a "name=modi" -b
   ```

6. Setup:
   Gathers all targets info

   ```sh
   ansible all -m setup
   ```

## Inventory

Inventory file is a collection od hosts which are managed by ansible control node.

> Default Location: `/etc/ansible/hosts`

you can use your own inventory file by using argument `-i` and `<path>` of your inventory file

```sh
ansible -i <path of inevntory file> -m user -a "name=<USER_NAME>" -b
```

## Custom ansible.cfg file

```sh
sudo vi /opt/ansible.config
```

You can change the default inventory file by replacing path of inventory in ansible.conf under [defaults]

### Order of using "ansible.cfg" file

* ANSIBLE_CONFIG (an environment variable)
* ansible.cfg ( in the current directory)
* .ansible.cfg ( in home directory)
* /etc/ansible/ansible.cfg

## Ansible Modules

Modules interact with your remote systems to perform specific tasks like

* creating users , installing packages, updating configuration, spinning up onstances, etc.,

Ansible comes with thousands of modules

## Ansible Playbook

* A playbook is a text file written in YAML format and is normally saved as .yml
* Begins with ---
* Starts with a single dash fillowed by a space
* hosts and tasks are mandatory items in playbook
* Playbook primarily uses indentation with two space characters to indicate the structure of its data
* Modules are used to perform tasks
* Comments starts with #
* Conditions: with_items, when, loop, notify & handlers
  
## Ansible Variables

* Define within the playbook
* Passing from external files
* Passing from hosts inventory
* Passing while running playbook
* Using group_vars and hosts_vars and so on

```sh
vars:
 user_name: modi
```

or

```sh
vars_files:
 - /home/ansadmin/user.yml
```

Using passed variables:

```sh
{{user_name}}
```

* group_vars
* host_vars

## Ansible vault

* create, view, edit, encrypt, decrypt, --ask-vault-pass, --vault-password-file

```sh
ansible-vault create vault.yml
```

Every ansible vault command is starting with ansible-vault

## Ansible Roles

To create a role use command

```sh
ansible-galaxy init <Your_Role_Name>
```

To install a role from galaxy server

```sh
ansible-galaxy install <your_role_url>
```

This saves the role at `/home/admin/.ansible/roles`

## Ansible Plugins to install in jenkins

### Publish over SSH plugin

`Publish over SSH`

To install/deploy artifacts using jenkins via ansible install a plugin `publish over ssh`, this plugin sends build artifacts to deploy
