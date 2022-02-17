## Installing, updating, and uninstalling the AWS CLI

### AWS CLI version 2

The AWS CLI version 2 is the most recent major version of the AWS CLI and supports all of the latest features. Some features introduced in version 2 are not backported to version 1 and you must upgrade to access those features.

#### Install the AWS CLI version 2 on Linux

Follow these steps from the command line to install the AWS CLI on Linux.

We provide the steps in one easy to copy and paste group based on whether you use 64-bit Linux or Linux ARM. See the descriptions of each line in the steps that follow.

1. For the latest version of the AWS CLI, use the following command block:

Use the curl command – The -o option specifies the file name that the downloaded package is written to. The options on the following example command write the downloaded file to the current directory with the local name awscliv2.zip.

***Linux x86 (64-bit):***
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```
***Linux ARM:***
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-aarch64.zip" -o "awscliv2.zip"
```
2. Unzip the installer. If your Linux distribution doesn't have a built-in unzip command, use an equivalent to unzip it. The following example command unzips the package and creates a directory named aws under the current directory.
```
unzip awscliv2.zip
```
3. Run the install program. The installation command uses a file named install in the newly unzipped aws directory. By default, the files are all installed to /usr/local/aws-cli, and a symbolic link is created in /usr/local/bin. The command includes sudo to grant write permissions to those directories.
```
sudo ./aws/install
```

You can install without sudo if you specify directories that you already have write permissions to.
Now log out of your shell and back in again.

4. Confirm the installation.
```
aws --version
```

### Update the AWS CLI version 1 to verison 2 on Linux

To update your copy of the AWS CLI version 1 to version 2, from the Linux command line, follow these steps.

1. Download the installation file in one of the following ways:

Using the curl command – The options on the following example command write the downloaded file to the current directory with the local name awscliv2.zip.

The -o option specifies the file name that the downloaded package is written to. In this example, the file is written to awscliv2.zip in the current directory.

***Linux x86 (64-bit):***
For the latest version of the AWS CLI, use the following command block:
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```
2. Unzip the installer. If your Linux distribution doesn't have a built-in unzip command, use an equivalent to install it. The following example command unzips the package and creates a directory named aws under the current directory.
```
unzip awscliv2.zip
```
3. To ensure that the update installs in the same location as your current AWS CLI version 1, locate the existing symlink and installation directory.
* Use the which command to find your symlink. This gives you the path to use with the --bin-dir parameter.
```
which aws
```
* Use the ls command to find the directory that your symlink points to. This gives you the path to use with the --install-dir parameter.
```
ls -l /usr/local/bin/aws
```
4. Use your symlink and installer information to construct the install command with the --update parameter.
```
sudo ./aws/install --bin-dir /usr/local/bin --install-dir /usr/local/aws-cli --update
```
5. Confirm the installation.
```
aws --version
```


## Uninstall the AWS CLI version 2 on Linux

### To uninstall the AWS CLI version 2, run the following commands.

1. Locate the symlink and install paths.

Use the which command to find the symlink. This shows the path you used with the --bin-dir parameter.
```
which aws
```

> OUTPUT: /usr/local/bin/aws

2. Use the ls command to find the directory that the symlink points to. This gives you the path you used with the --install-dir parameter.
```
ls -l /usr/local/bin/aws
```
> lrwxrwxrwx 1 ec2-user ec2-user 49 Oct 22 09:49 /usr/local/bin/aws -> /usr/local/aws-cli/v2/current/bin/aws

3. Delete the two symlinks in the --bin-dir directory. If your user account has write permission to these directories, you don't need to use sudo.
```
sudo rm /usr/local/bin/aws
sudo rm /usr/local/bin/aws_completer
```
4. Delete the --install-dir directory. If your user account has write permission to this directory, you don't need to use sudo.
```
sudo rm -rf /usr/local/aws-cli
```