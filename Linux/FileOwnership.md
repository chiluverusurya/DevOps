# Ownership of file or directory

> ***Note***: Only root user can change the ownership of a file or a directory

```sh
chown <user>:<group> <filename>
```

Example:
> chown john:john file1

Changes user and group ownership

> chown john file2

Changes user ownership but group remains same

>***Note:***
To change permissions of a file, user must be owner or a root user. But to change ownership the user must and should be a root user.
