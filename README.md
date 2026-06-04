# Docker Install

```bash
dnf -y install dnf-plugins-core

dnf config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo

dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

systemctl start docker
systemctl enable docker

usermod -aG docker ec2-user

mkdir -p $HOME/bin
sudo cp ./kubectl /usr/local/bin/

export PATH=$HOME/bin:$PATH
```

# EKSCTL Install

```bash
ARCH=amd64
PLATFORM=$(uname -s)_$ARCH

curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_${PLATFORM}.tar.gz"

tar -xzf eksctl_${PLATFORM}.tar.gz -C /tmp

sudo install -m 0755 /tmp/eksctl /usr/local/bin

rm -f eksctl_${PLATFORM}.tar.gz
rm -f /tmp/eksctl
```

# Kubens Install

```bash
sudo git clone https://github.com/ahmetb/kubectx /opt/kubectx

# Partition Extension

```bash id="n2h1jy"
sudo growpart /dev/nvme0n1 4

sudo lvextend -L +30G /dev/mapper/RootVG-varVol

sudo xfs_growfs /var
```

# Helm Installation

```bash id="r8y6d5"
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-4

chmod 700 get_helm.sh

./get_helm.sh
```


sudo ln -s /opt/kubectx/kubens /usr/local/bin/kubens
```
