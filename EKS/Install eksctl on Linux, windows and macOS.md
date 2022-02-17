## The eksctl command line utility

`eksctl` is a simple command line utility for creating and managing Kubernetes clusters on Amazon EKS. The eksctl command line utility provides the fastest and easiest way to create a new cluster with nodes for Amazon EKS.

For more information and to see the official documentation, visit [https://eksctl.io/](https://eksctl.io/) or [https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html](https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html).

### Installing or upgrading eksctl

Install or upgrade the latest version of the eksctl command line utility.

#### To install or upgrade eksctl on Linux using curl

*** Linux: ***

1. Download and extract the latest release of eksctl with the following command.
```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
```
2. Move the extracted binary to /usr/local/bin.
```
sudo mv /tmp/eksctl /usr/local/bin
```
3. Test that your installation was successful with the following command.
```
eksctl version
```
> **Note:** The GitTag version should be at least 0.83.0. If not, check your terminal output for any installation or upgrade errors, or replace the address in step 1 with https://github.com/weaveworks/eksctl/releases/download/v0.83.0/eksctl_Linux_amd64.tar.gz and complete steps 1-3 again.

#### To install or upgrade eksctl on Windows using Chocolatey

*** Windows: ***

1. If you do not already have Chocolatey installed on your Windows system, see [Installing Chocolatey](https://chocolatey.org/install).
2. Install or upgrade `eksctl`.
* Install the binaries with the following command:
```
choco install -y eksctl 
```
* If they are already installed, run the following command to upgrade:
```
choco upgrade -y eksctl 
```
3. Test that your installation was successful with the following command.
```
eksctl version
```

> **Note:** The GitTag version should be at least 0.83.0. If not, check your terminal output for any installation or upgrade errors, or manually download an archive of the release from https://github.com/weaveworks/eksctl/releases/download/v0.83.0/eksctl_Windows_amd64.zip, extract eksctl, and then run it.

#### To install or upgrade eksctl on macOS using Homebrew

*** MacOs: ***

The easiest way to get started with Amazon EKS and macOS is by installing `eksctl` with [Homebrew](https://brew.sh/). The eksctl Homebrew recipe installs eksctl and any other dependencies that are required for Amazon EKS, such as `kubectl`. The recipe also installs the [aws-iam-authenticator](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html), which is required if you don't have the AWS CLI version 1.16.156 or higher installed.

1. If you do not already have Homebrew installed on macOS, install it with the following command.
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```
2. Install the Weaveworks Homebrew tap.

```
brew tap weaveworks/tap
```
3. Install or upgrade `eksctl`.
* Install eksctl with the following command:
```
brew install weaveworks/tap/eksctl
```
* If eksctl is already installed, run the following command to upgrade:
```
brew upgrade eksctl && brew link --overwrite eksctl
```
4. Test that your installation was successful with the following command.
```
eksctl version
```

> ** Note: ** The GitTag version should be at least 0.83.0. If not, check your terminal output for any installation or upgrade errors, or manually download an archive of the release from https://github.com/weaveworks/eksctl/releases/download/v0.83.0/eksctl_Darwin_amd64.tar.gz, extract eksctl, and then run it.
