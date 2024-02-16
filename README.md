# Valheim

## Installation

This tutorial is a quick note for a basic installation of a valheim server from scratch on Rhel9 or Centos Stream 9. [This image](https://github.com/mbround18/valheim-docker) released by mbround18  has BepInEx support and is compatible with [ValheimPlus last release by Grantapher](https://github.com/Grantapher/ValheimPlus/blob/grantapher-development) as it is showed here.

### Prerequisites

```bash
sudo yum update -y

sudo timedatectl set-timezone  Europe/Paris

sudo yum install -y yum-utils

sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y 
```

### Main install

```bash
sudo usermod -aG docker ${USER}
```

```bash
# Create main dir
mkdir -p ./valheim
```

```bash
# Write docker-compose file
vi docker-compose.yml
```

```bash
# For rootless execution of container
sudo yum -y install docker-ce-rootless-extras
```

```bash
# Add exposed ports to public zone
sudo firewall-cmd --add-port 2456-2458/udp --zone=public --permanent
```

```bash
# make container run in background while user is disconnected
loginctl enable-linger $UID
```

```bash
# Launch once to create directory tree
docker compose up -d
```

```bash
# Customize valheim.cfg file 
sudo vi ./valheim/server/BepInEx/config/valheim_plus.cfg
```

```bash
# Restart container
docker compose down && docker compose up -d
```

## Personnal customizations :

```bash
# Used for restart of container due to low profile of virtual machine
0 4 */4 * * docker compose down && docker compose up -d
```