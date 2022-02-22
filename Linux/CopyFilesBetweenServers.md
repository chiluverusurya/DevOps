# Copy files between servers

## Windows to Linux

* Mobaxterm or winscp

## Linux to linux

* scp (secure copy) is a command-line utility that allows you to securely copy file and directories between two systems.

```bash
scp <source_file_name> username@<dest_host>:<dest_folder>
```

Example:
copy file to remote server from local server
> scp file1 root@10.20.30.40:/tmp

copy file from remote server to local server
>scp root@10.20.30.40:/tmp /home/ec2-user

### To copy directories use flag with argument "r"

```bash
scp -r <src_dir> usr@hostname:/<dest_folder>
```
