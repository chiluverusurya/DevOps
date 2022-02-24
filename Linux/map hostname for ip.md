# Mapping Hostname for Host Ip Address

## For hostname

Add an entry in /etc/hosts file on the system you're ssh'ing from.

The syntax is

```text
<IP_ADDRESS> <HOSTNAME>
```

> Example: `10.10.100.1 WebServer`

This works on Linux and Mac. For Windows, the file is c:\windows\system\drivers\etc\hosts.

## For SSH'ing

If you only want the name for ssh and ssh only, you can add a name to your ssh config in ~/.ssh/config

As an example, your config file could look like this:

```text
Host database
    HostName <real_IP_address/hostname>
    User username
```

Then you can type ssh database on the command line and ssh will automatically do ssh username@ip.address for you.

Example:
`ssh database`
