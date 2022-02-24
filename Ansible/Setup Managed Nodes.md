# Setup Managed Node or Target Node

Repeat the same steps used in controlled node to setup hostname(different hostname) and create users with root access and enable password based login

Copy the public ssh key (id_rsa.pub) from control node to the taget node or managed node (Path = /.ssh/authurized_keys) or else enter the command from control node

```sh
ssh-copy-id <user_name>@<target_ip>
```

   or

```sh
ssh-copy-id <target-server>
```

> ***Note:*** SSH service must be reoladed to execute this operation(`service sshd reload`)

You can get the ip address of target node by using 'ip addr' command in target node

This is a private ip address only works if and only target and control nodes are in same vpc otherwise use public ip. Private ip is safer ot use than public ip

## Login to managed node from control node

```sh
ssh <target_ip_address>
```

  or

```sh
ssh <user_name>@<ip_address> #ssh ansadmin@<ip_address>
```

  or

```sh
ssh -i .ssh/id_rsa <user_name>@<ip_address>
```

### Adding managed nodes to ansible or control node or master node

```sh
cd /etc/ansible
sudo vi hosts
```

(Delete content of file and add ip_address of managed nodes)

```sh
cat hosts
```

### Do a Ping test

```sh
ansible all -m ping
```
