# Installing Ansible(v2.10.8)

## Prerequisites

1. Python

## Setup hostname (Optional but useful)

```sh
sudo su -
vi /etc/hostname
```

Replace the existing hostname with your desired hostname such as AnsibleServer/ControlNode/MasterNode.

## Create a new user

```sh
useradd ansadmin
passwd ansadmin
```

## Add user to sudoers file and grant root access

Grant new user:admin root access by editing `/etc/sudoers` file using `visudo`

> ***Note***: Always use `visudo` to edit sudoers file

```sh
visudo
```

### Edit and add below statements at the end of the file

```sh
ansadmin ALL=(ALL:ALL) ALL
ansadmin ALL=(ALL)  NOPASSWD: ALL
```

> root   ALL=(ALL:ALL) ALL

This means that our root user can run any command using sudo, as long as they provide their password.

1. The first field indicates the username that the rule will apply to (root).
2. The first “ALL” indicates that this rule applies to all hosts.
3. Second “ALL” indicates that the root user can run commands as all users
4. Third “ALL” indicates that the root user can run commands as all groups.
5. The last “ALL” indicates these rules apply to all commands

> user_name ALL=(ALL) NOPASSWD: ALL

This means that our root user can run any command using sudo, without providing their password.

## Enable Password based login

```sh
vi /etc/ssh/sshd_config
```

Search for keyword `/Password` and replace `PasswordAuthentication no` to `PasswordAuthentication yes` then save and exit the file

### Reload the file to effect the changes

```sh
service sshd reload
```

Using keybased authentication is advised. If you are still at learning stage use password based authentication (Master & Slave)

### You can also try below sed command which replaces "PasswordAuthentication no to yes" without editing file

```sh
sed -ie 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
```

## Generate SSH keys

First login as ansadmin to generate ssh key for ansadmin

```sh
su - ansadmin
```

Generate ssh keys for ansadmin

```sh
ssh-keygen
```

Two keys id_rsa (private_key) and id_rsa.pub (public key) are generated

Later you will need to copy this public-key id_rsa.pub to all managed_nodes/target_nodes.

## Install Python

You need to install python before installing ansible

### Check for python installation

```sh
 python --version
```

If not exist install python, Use below command with respect to your os:

***CentOs:***

```sh
sudo yum install python3
```

***Debian:***

```sh
sudo apt-get install python3
```

### Now check again for python installation

```sh
python --version
```

Goto official ansible website to know updated installation commands and latest version

## Installing and upgrading Ansible with pip

Ansible can be installed on many systems with pip, the Python package manager.

### Installing pip

If your Python environment does not have pip installed, there are 2 mechanisms to install pip supported directly by pip’s maintainers:

* ensurepip
* get-pip.py

### ensurepip

Python comes with an ensurepip module1, which can install pip in a Python environment.

```sh
python -m ensurepip --upgrade
```

More details about how ensurepip works and how it can be used, is available in the standard library documentation.

### get-pip.py

This is a Python script that uses some bootstrapping logic to install pip.

Download the script, from <https://bootstrap.pypa.io/get-pip.py>

Open a terminal/command prompt, cd to the folder containing the get-pip.py file and run:

```sh
python get-pip.py
```

### Installing ansible using pip

Once pip is installed, you can install Ansible:

```sh
python -m pip install --user ansible
```

If you wish to install Ansible globally, run the following commands:

```sh
sudo python -m pip install ansible
```

Check the installed version

```sh
ansible --version
```

Default directory of ansible is at `/etc/ansible`

Ansible has been successfully installed and configured.
