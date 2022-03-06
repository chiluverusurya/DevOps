# Install Docker on Debian (Ubuntu)

To get started with Docker Engine on Debian, make sure you meet the [prerequisites](https://docs.docker.com/engine/install/debian/#prerequisites), then install Docker.

## Uninstall old versions

Older versions of Docker were called docker, docker.io, or docker-engine. If these are installed, uninstall them:

```sh
sudo apt-get remove docker docker-engine docker.io containerd runc
```

It’s OK if apt-get reports that none of these packages are installed.

The contents of `/var/lib/docker/`, including images, containers, volumes, and networks, are preserved. The Docker Engine package is now called `docker-ce`.

## Installation methods

You can install Docker Engine in different ways, depending on your needs:

1. Most users set up Docker’s repositories and install from them, for ease of installation and upgrade tasks. This is the recommended approach, except for Raspbian.
2. Some users download the DEB package and install it manually and manage upgrades completely manually. This is useful in situations such as installing Docker on air-gapped systems with no access to the internet.
3. In testing and development environments, some users choose to use automated convenience scripts to install Docker. This is currently the only approach for Raspbian.

## Install using the repository

Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

> **Raspbian users cannot use this method!**
For Raspbian, installing using the repository is not yet supported. You must instead use the convenience script.

1. Set up the repository
   Update the apt package index and install packages to allow apt to use a repository over HTTPS:

   ```sh
   sudo apt-get update
   sudo apt-get install ca-certificates curl gnupg lsb-release
   ```

   Add Docker’s official GPG key:

   ```sh
   curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   ```

   Use the following command to set up the stable repository. To add the nightly or test repository, add the word nightly or test (or both) after the word stable in the commands below. Learn about nightly and test channels.

   ```sh
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```

2. Install Docker Engine
   This procedure works for Debian on x86_64 / amd64, armhf, arm64, and Raspbian.

   * Update the apt package index, and install the latest version of Docker Engine and containerd, or go to the next step to install a specific version:

   ```sh
   sudo apt-get update
   sudo apt-get install docker-ce docker-ce-cli containerd.io
   ```

   ***Got multiple Docker repositories?***
   > If you have multiple Docker repositories enabled, installing or updating without specifying a version in the apt-get install or apt-get update command always installs the highest possible version, which may not be appropriate for your stability needs.

   ***Receiving a GPG error when running apt-get update?***
   > Your default umask may not be set correctly, causing the public key file for the repo to not be detected. Run the following command and then try to update your repo again: sudo chmod a+r /usr/share/keyrings/docker-archive-keyring.gpg.

   * To install a specific version of Docker Engine, list the available versions in the repo, then select and install:

   a. List the versions available in your repo:

   ```sh
   apt-cache madison docker-ce
   ```

   b. Install a specific version using the version string from the second column, for example, 5:18.09.1 ~3-0~debian-stretch .

   ```sh
   sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
   ```

   * Verify that Docker Engine is installed correctly by running the hello-world image.

   ```sh
   sudo docker run hello-world
   ```

   This command downloads a test image and runs it in a container. When the container runs, it prints a message and exits.

   Docker Engine is installed and running. The `docker` group is created but no users are added to it. You need to use `sudo` to run Docker commands. Continue to Linux postinstall to allow non-privileged users to run Docker commands and for other optional configuration steps.

3. Upgrade Docker Engine
   To upgrade Docker Engine, first run `sudo apt-get update`, then follow the installation instructions, choosing the new version you want to install.

## Install from a package

If you cannot use Docker’s repository to install Docker Engine, you can download the `.deb` file for your release and install it manually. You need to download a new file each time you want to upgrade Docker.

1. Go to <https://download.docker.com/linux/debian/dists/>, choose your Debian version, then browse to pool/stable/, choose amd64, armhf, or arm64, and download the .deb file for the Docker Engine version you want to install.

   ***Note:***
   > To install a nightly or test (pre-release) package, change the word stable in the above URL to nightly or test. Learn about nightly and test channels.

2. Install Docker Engine, changing the path below to the path where you downloaded the Docker package.

   ```sh
   sudo dpkg -i /path/to/package.deb
   ```

   The Docker daemon starts automatically.

3. Verify that Docker Engine is installed correctly by running the hello-world image.

   ```sh
   sudo docker run hello-world
   ```

   This command downloads a test image and runs it in a container. When the container runs, it prints a message and exits.

   > Docker Engine is installed and running. The `docker` group is created but no users are added to it. You need to use `sudo` to run Docker commands. Continue to Post-installation steps for Linux to allow non-privileged users to run Docker commands and for other optional configuration steps.

4. Upgrade Docker Engine
   To upgrade Docker Engine, download the newer package file and repeat the installation procedure, pointing to the new file.

## Install using the convenience script

Docker provides a convenience script at get.docker.com to install Docker into development environments quickly and non-interactively. The convenience script is not recommended for production environments, but can be used as an example to create a provisioning script that is tailored to your needs. Also refer to the install using the repository steps to learn about installation steps to install using the package repository. The source code for the script is open source, and can be found in the `docker-install` repository on GitHub.

Always examine scripts downloaded from the internet before running them locally. Before installing, make yourself familiar with potential risks and limitations of the convenience script:

* The script requires root or sudo privileges to run.
* The script attempts to detect your Linux distribution and version and configure your package management system for you, and does not allow you to customize most installation parameters.
* The script installs dependencies and recommendations without asking for confirmation. This may install a large number of packages, depending on the current configuration of your host machine.
* By default, the script installs the latest stable release of Docker, containerd, and runc. When using this script to provision a machine, this may result in unexpected major version upgrades of Docker. Always test (major) upgrades in a test environment before deploying to your production systems.
* The script is not designed to upgrade an existing Docker installation. When using the script to update an existing installation, dependencies may not be updated to the expected version, causing outdated versions to be used.

> ***Tip: preview script steps before running***
 You can run the script with the DRY_RUN=1 option to learn what steps the script will execute during installation:

 ```sh
 curl -fsSL https://get.docker.com -o get-docker.sh
 DRY_RUN=1 sh ./get-docker.sh
 ```

This example downloads the script from get.docker.com and runs it to install the latest stable release of Docker on Linux:

 ```sh
 curl -fsSL https://get.docker.com -o get-docker.sh
 sudo sh get-docker.sh
 ```

Docker is installed. The `docker` service starts automatically on Debian based distributions. On `RPM` based distributions, such as CentOS, Fedora, RHEL or SLES, you need to start it manually using the appropriate `systemctl` or `service` command. As the message indicates, non-root users cannot run Docker commands by default.

> ***Use Docker as a non-privileged user, or install in rootless mode?***

 The installation script requires root or sudo privileges to install and use Docker. If you want to grant non-root users access to Docker, refer to the post-installation steps for Linux. Docker can also be installed without root privileges, or configured to run in rootless mode. For instructions on running Docker in rootless mode, refer to run the Docker daemon as a non-root user (rootless mode).

## Uninstall Docker Engine

1. Uninstall the Docker Engine, CLI, and Containerd packages:

   ```sh
   sudo apt-get purge docker-ce docker-ce-cli containerd.io
   ```

2. Images, containers, volumes, or customized configuration files on your host are not automatically removed.

   To delete all images, containers, and volumes:

   ```sh
   sudo rm -rf /var/lib/docker
   sudo rm -rf /var/lib/containerd
   ```

   You must delete any edited configuration files manually.
