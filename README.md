<p align="right">
    <img src="https://github.com/AnastasiaTECHWRITER/create-and-deploy-image/assets/134202043/6559f7e9-2e21-4fb0-9a96-d0ff531b8ed8" width="55" height="55">
</p>

# Create and deploy image
This article contains the instructions on how to prepare the container image file and your IT infrastructure, and then deploy this image to Kubernetes.
<details open>
<summary>What is Kubernetes?</summary>
<br>
Kubernetes is an open-source container-orchestration tool designed by Google. It allows running your applications across on-site deployments and public clouds, and supports hybrid scenarios. Read the following Google documentation article to learn more about Kubernetes: https://cloud.google.com/learn/what-is-kubernetes.
</details>

##Install Docker
Install Docker Desctop, depending on your OS:
**For Windows:**
1. Make sure you meet the [installation requirements](https://docs.docker.com/desktop/install/windows-install/#system-requirements).
2. [Download](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe) Docker Desktop for Windows.
3. Follow the [installation prompts](https://docs.docker.com/desktop/install/windows-install/#install-docker-desktop-on-windows) (both: interactive and command prompt deployment scenario are supported).
**For Linux:**
1. Make sure you meet the [installation requirements](https://docs.docker.com/desktop/install/linux-install/#system-requirements).
2. Download the distributive and follow the installation prompts depending on your Linux distribution:
 - [Debian](https://docs.docker.com/desktop/install/debian/)
 - [Fedora](https://docs.docker.com/desktop/install/fedora/)
 - [Ubunty](https://docs.docker.com/desktop/install/ubuntu/)
 - [Arch](https://docs.docker.com/desktop/install/archlinux/)

## Create cataglogues
Create the directories where the application code, Docker resources and the Dockerfile will be located. You can keep all reources in the root folder, however, the example shows the structure with a dedicated directory for each resource:

