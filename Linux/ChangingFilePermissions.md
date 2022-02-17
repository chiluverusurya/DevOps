# File Permissions (Access modes)

Permissions are applied at three levels.
	- Owner or user levels
	- Group levels
	- Others level

Permissions are applied in three ways.
	- r - read only
	- w - write/edit/append/delete
	- x - execute/run

Access modes are different on file and directory

| Permissions | Files | Directory |
| :---------- | :---- | :-------- |
| r | opens the file | 'ls' the contents of directory |
| w | write/edit/append/delete | add/delete/remame contents of directory |
| x | to run a command or hell script | to enter into directory using 'cd' command |

File types available in linux operating system.

| Symbol | Type of file |
| ------ | ------------ |
| - | normal file |
| b | block file (hard disk, floppy disk) |
| c | character file (keyboard, mouse) |
| d | directory |
| l | link files (short cut ) |

# Changing Permissions
Permissions can be set on any file or directory by using two methods
	* Symbolic method (ugo)
	* Absolute method (numbers)

### Symbolic Method:

We use symbols u, g, o.
```
chmod [who] [+/-/=] [permissions] <file_name>
```

who --> to whom the permission to be assigned.
Permissions --> user/owner/(u); group(g); others(o)

Example:
> chmod u=rwx, g=rw, o=r <file_name>
or
> chmod ugo=rwx <file_name>

### Absolute Method:

We use numbers instead of sylmbols

Read	- 4
Write	- 2
Execute	- 1

```
chmod <numbers> <file_name>
```

Example:
>chmod 764 <file_name>

Note: To change permission you should either be the owner of the file or a root user.