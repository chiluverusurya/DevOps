# Installing Docker on Amazon Linux 2

To install amazon-linux-extras, verify connection to the internet from within the instance then check the instance's OS

```sh
cat /etc/os-release
```

If the OS is amazon linux version 2 run

```sh
sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
```

Or run

```sh
sudo yum-config-manager --enable epel
```

To use the EPEL repository. You can now install available packages.

```sh
sudo amazon-linux-extras install docker
```

see [aws documentation]( https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/amazon-linux-ami-basics.html#extras-library ) for more details.

Start Docker.

```sh
sudo systemctl start docker
```

Verify that Docker Engine is installed correctly by running the hello-world image.

```sh
sudo docker run hello-world
```
