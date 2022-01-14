# Linux File System Hierarchy

| Directory Name | Description |
| :------------: | :--------- |
| / | <ul><li>This is a top level directory.</li><li>It is a parent directory for all other directories.</li><li>It is called ROOT directory.</li><li>It is represented by forward slash "/".</li><li>In windows it is " c:\ ". </li></ul> |
| /root | <ul><li>It is home directory for root user ( super user ).</li><li>It provides working environment for root user.</li><li>In windoes it is " c:\users\adminstrator ".</li></ul> |
| /home | <ul><li>It is home directory for other users.</li><li>It provides working environment for other users ( other than root user ).</li><li>In windows it is " c:\users/user ".</li></ul> |
| /usr | <ul><li>By default softwares are installed in /usr directory (UNIX sharable resources).</li><li>In windows it is " c:\program files ".</li></ul> |
| /bin | <ul><li>It contains commands used by all users ( Binary files ).</li></ul> |
| /sbin | <ul><li>It contains commands used by only super user (root) (super user binary files).</li></ul> |
| /var | <ul><li>It contains variable data like mails, log files.</li></ul> |
| /boot | <ul><li>Contains boot loader files (ex: kernels, initrd, grub files).</li></ul> |
| /dev | <ul><li>Contains esential device files.</li><li>These include terminal devices, usb or any other attached devices to the system. ( /dev/ttyl, /dev/usbmon0 ).</li></ul> |
| /etc | <ul><li>Contains host-specific system-wide cofiguration files required by all programs.</li></ul> |
| /lib | <ul><li>Contains liraries essential for the binaries in /bin and /sbin.</li><li>library filenames are either ld* or lib*.so.*</li><li>Ex: ld-211.1.so, libcurses.so.5.7</li></ul> |
| /media | <ul><li>Temporary mount directories for removable devices. (Ex: CD-ROMS ).</li></ul> |
| /mnt | <ul><li>Temporarily mounted filesystems.</li><li>Temporarily mount directories where sysadmins can mount filesystems.</li></ul> |
| /opt | <ul><li>Optional application software packages.</li></ul> |
| /srv | <ul><li>srv stands for service.</li><li>Contains service specific related data such as data and scripts for web and ftp servers.</li></ul> |
| /tmp | <ul><li>Contains temporary files.</li><li>Deleted automatically after system reboot.</li></ul> |
| /proc | <ul><li>Contains info about system process.</li></ul> |