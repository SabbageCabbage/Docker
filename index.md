# Docker Installation + Folding@home Installation Guide (Debian)

## Docker Installation
Visit https://docs.docker.com/engine/install to find instructions for your specific distro.
### Uninstall Potential Conflicting Packages 

    sudo apt remove $(dpkg --get-selections docker.io docker-compose docker-doc podman-docker containerd runc | cut -f1)
###  Set up Docker's apt repository.

    # Add Docker's official GPG key:
    sudo apt update
    sudo apt install ca-certificates curl
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc

### Add the repository to Apt sources:
    sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
    Types: deb
    URIs: https://download.docker.com/linux/debian
    Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
    Components: stable
    Signed-By: /etc/apt/keyrings/docker.asc
    EOF
    sudo apt update

### Install the Docker packages
    sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

### Verify that Docker is running
    sudo systemctl status docker

## 💥 LET'S FOLD SOME PROTEIN 💥

### Account Creation
Create your account at https://v8-4.foldingathome.org/machines

### Make Your Directory 
    mkdir -p ~/docker-projects/folding@home
    cd ~/docker-projects/folding@home

### Create your .yml file 
Use a text editor to create your docker-compose file and add the following:

    services:
      foldingathome:
        image: lscr.io/linuxserver foldingathome:latest
        container_name: foldingathome
        environment:
          - PUID=1000
          - PGID=1000
          - TZ=Etc/UTC
          - ACCOUNT_TOKEN= #Grabbed from the account that you created by using the link above 
          - MACHINE_NAME=
          - CLI_ARGS= #optional
        volumes:
          - /path/to/foldingathome/data:/config
        ports:
          - 7396:7396 #optional
        restart: unless-stopped

**Side note**: If you have an NVIDIA gpu and want to utilize hardware acceleration you'll have to install the container runtime from NVIDIA here's the link to some instructions to do that:
https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html

you'll also have to add:

    --runtime=nvidia -e 
    NVIDIA_VISIBLE_DEVICES=all 

to your docker-compose file 

### Starting
   
    sudo docker compose up -d

### Make sure its running

    sudo docker ps 

Once it's running you can visit:
    
    localhost:7396

and edit your machine settings :>

### Examples of what that should look like 
![alt text](<Screenshot from 2025-11-16 00-27-48.png>)

![alt text](<Screenshot from 2025-11-16 00-29-20.png>)
