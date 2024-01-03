markdown

# How to Install Portainer on Docker

*by Blog Edu Tech, January 14, 2022*

To install Portainer on Docker, follow these steps:

1. **Connect (log on) to the VPS server** using Putty or another SSH client.
2. **Check if Docker is installed** by running the appropriate command.
3. Run the following Docker commands:
   
   ```bash
   docker volume create portainer_data
   
   docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always \
   -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data \
   portainer/portainer-ce:2.9.3

    Access your Portainer Server instance by opening a web browser and navigating to:

    plaintext

    http://ip_of_the_vps:9000

    Replace ip_of_the_vps with the actual IP address of your VPS.

Once Portainer is installed, you can use the web interface by accessing the specified IP address on port 9000 through your browser.

Additionally, after installing Portainer, you can install Nginx Proxy Manager, which is a GUI for Docker containers. If you plan to install Nginx Proxy Manager on Portainer, follow the tutorial: How to install Nginx Proxy Manager on Portainer.
