## Installing kubectl

Kubernetes uses a command line utility called kubectl for communicating with the cluster API server. The kubectl binary is available in many operating system package managers, and this option is often much easier than a manual download and install process. You can follow the instructions for your specific operating system or package manager in the [Kubernetes documentation](https://kubernetes.io/docs/tasks/tools/) to install.

> **Note:** You must use a kubectl version that is within one minor version difference of your Amazon EKS cluster control plane. For example, a v1.23 client can communicate with v1.22, v1.23, and v1.24 control planes.

The following methods exist for installing kubectl on Linux:

* [Install kubectl binary with curl on Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-kubectl-binary-with-curl-on-linux)
* [Install using native package management](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-using-native-package-management)
* [Install using other package managemen](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-using-other-package-management)

### Install kubectl binary with curl on Linux

Warning: check the current default kubernetes version supplied with EKS and install a matching version of kubectl

1. Download the latest release with the command:
From official Kubernetes:
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```
> ***Note:*** To download a specific version, replace the $(curl -L -s https://dl.k8s.io/release/stable.txt) portion of the command with the specific version.
> For example, to download version v1.23.0 on Linux, type:
> ```curl -LO https://dl.k8s.io/release/v1.23.0/bin/linux/amd64/kubectl```

From AWS:
Download the Amazon EKS vended kubectl binary for your cluster's Kubernetes version from Amazon S3 using the command for your hardware platform.
```
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.21.2/2021-07-05/bin/linux/amd64/kubectl
```
2. Validate the binary (optional)
Verify the downloaded binary with the SHA-256 sum for your binary.

Download the kubectl SHA-256 checksum file:

From offiial kubernetes:
```
curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
```
Validate the kubectl binary against the checksum file:
For Kubernetes downloaded binaries:
```
echo "$(<kubectl.sha256)  kubectl" | sha256sum --check
```
If valid, the output is:

```
kubectl: OK
```
If the check fails, sha256 exits with nonzero status and prints output similar to:
```
kubectl: FAILED
sha256sum: WARNING: 1 computed checksum did NOT match
```
> Note: Download the same version of the binary and checksum.

From AWS:
* Download the SHA-256 sum for your cluster's Kubernetes version for Linux using the command for your hardware platform.
```
curl -o kubectl.sha256 https://amazon-eks.s3.us-west-2.amazonaws.com/1.21.2/2021-07-05/bin/linux/amd64/kubectl.sha256
```

* Check the SHA-256 sum for your downloaded binary.
```
openssl sha1 -sha256 kubectl
```
* Compare the generated SHA-256 sum in the command output against your downloaded SHA-256 file. The two should match.

3. Apply execute permissions to the binary.
```
chmod +x ./kubectl
```

4. Install kubectl

For Official kubernetes:

```
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

> ***Note:***
> If you do not have root access on the target system, you can still install kubectl to the ~/.local/bin directory:
> ```
> chmod +x kubectl
> mkdir -p ~/.local/bin/kubectl
> mv ./kubectl ~/.local/bin/kubectl
> # and then append (or prepend) ~/.local/bin to $PATH
>```

For AWS:
Copy the binary to a folder in your PATH. If you have already installed a version of kubectl, then we recommend creating a $HOME/bin/kubectl and ensuring that $HOME/bin comes first in your $PATH.
```
mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$PATH:$HOME/bin
```
(Optional) Add the $HOME/bin path to your shell initialization file so that it is configured when you open a shell.
```
echo 'export PATH=$PATH:$HOME/bin' >> ~/.bashrc
```

After you install kubectl, you can verify its version with the following command:

```
kubectl version --client
```
		or
```
kubectl version --short --client
```