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

## :boom: LET'S FOLD SOME PROTEIN :boom: