# DOCKER Install

# Set up the repository
Install the dnf-plugins-core package (which provides the commands to manage your DNF repositories) and set up the repository.
```
dnf -y install dnf-plugins-core

dnf config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo
```
Install the Docker packages
```
dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```
Start Docker Engine
```
systemctl start docker
```
Start Enable Engine
```
systemctl enable docker
```
Add ec2-user to the Docker group so Docker commands can be executed without sudo
```
usermod -aG docker ec2-user
```


# EKSCTL Install
# The following commands download and install the latest version of eksctl, a command-line tool used to create and manage Amazon EKS clusters

Sets the CPU architecture
```
ARCH=amd64
```
 Detects the operating system and architecture (e.g., Linux_amd640)
```
PLATFORM=$(uname -s)_$ARCH
```
Downloads the latest eksctl package
```
curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"
```
Extracts the downloaded archive
```
tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz
```
Installs eksctl to /usr/local/bin & Removes temporary files after installation
```
sudo install -m 0755 /tmp/eksctl /usr/local/bin && rm /tmp/eksctl
```

# Kubens Install
 kubens is a command-line utility that helps Kubernetes users quickly switch between namespaces. It is part of the kubectx project

```
sudo git clone https://github.com/ahmetb/kubectx /opt/kubectx
```
```
sudo ln -s /opt/kubectx/kubens /usr/local/bin/kubens
```

# Helm Installation
 ## Helm now has an installer script that will automatically grab the latest version of Helm and install it locally.

You can fetch that script, and then execute it locally. It's well documented so that you can read through it and understand what it is doing before you run it
```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-4

chmod 700 get_helm.sh

./get_helm.sh
```

# KUBECTL INSTALL
## Download the latest release with the command
kubectl is the official Kubernetes command-line tool used to deploy applications, inspect cluster resources, manage workloads, and interact with Kubernetes clusters
```
curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.34.2/2025-11-13/bin/linux/amd64/kubectl
```
Grants execute permissions to the downloaded binary
```
chmod +x ./kubectl
```
Moves the binary to a system-wide executable path
```
sudo mv kubectl /usr/local/bin/
```
Sets up the kubectl binary and configures the environment for easy command execution
```
mkdir -p $HOME/bin && cp ./kubectl  /usr/local/bin && export PATH=$HOME/bin:$PATH
```
Copies the kubectl binary to /usr/local/bin, making it available as a system-wide executable command
```
sudo cp ./kubectl /usr/local/bin/
```
---
# Alternative Installation: Use a locally available kubectl binary and configure it for system-wide access without downloading it again

Creates the user's local binary directory if it does not exist
```
mkdir -p $HOME/bin
```
Copies the kubectl binary to a system executable path
```
sudo cp ./kubectl /usr/local/bin/
```
Updates the PATH environment variable to include the user's local binary directory.
```
export PATH=$HOME/bin:$PATH
```

#  PARTITION

Extends partition 4 to utilize the newly available disk space
```
sudo growpart /dev/nvme0n1 4
```
Increases the size of the /var logical volume by 30 GB
```
sudo lvextend -L +30G /dev/mapper/RootVG-varVol
```
Expands the XFS filesystem on /var to use the newly allocated space
```
sudo xfs_growfs /var
```
----
Increases the size of the /home logical volume
```
sudo lvextend -L +10G /dev/mapper/RootVG-homeVol
```
Increases the size of the root (/) logical volume
```
sudo lvextend -L +10G /dev/mapper/RootVG-rootVol
```
Expands the XFS filesystem on /home to use the newly allocated space
```
sudo xfs_growfs /home
```
Expands the root filesystem to utilize the additional logical volume space
```
sudo xfs_growfs /
```
