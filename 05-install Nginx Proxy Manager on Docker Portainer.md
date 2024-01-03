
# How to install Nginx Proxy Manager on Docker Portainer

## By Blog Edu Tech
## January 14, 2022

### Prerequisites:

* A Linux machine or virtual machine in the cloud
* Docker and Docker-compose installed
* Portainer installed on Docker

### Steps:

1. **Deploy NPM through Portainer:**

   - Open Portainer and navigate to **Stacks** > **Add stack**.
   - Paste the following Docker Compose configuration:

   ```yaml
   version: '3'
   services:
     app:
       image: 'jc21/nginx-proxy-manager:latest'
       restart: unless-stopped
       ports:
         - '80:80'
         - '81:81'
         - '443:443'
       volumes:
         - ./data:/data
         - ./letsencrypt:/etc/letsencrypt
   

2. **Open ports:**

   - Allow traffic through ports 80 (HTTP), 443 (HTTPS), and 81 (NPM admin UI).

3. **Access the NPM admin UI:**

   - Visit `http://ip_of_the_server:81` in your browser.
   - Use default credentials:
     - Email: `admin@example.com`
     - Password: `changeme`

4. **Change default credentials:**

   - Immediately upon login, you'll be prompted to modify details and change the password.
   - Sign out and log back in with the new credentials.

5. **Secure server with Cloudflare and NPM:**

   - Add your domain name to Cloudflare.
   - Update the IP address in Cloudflare DNS settings (DNS only).
   - In NPM, create a proxy host:
     - Domain name
     - HTTP
     - IP address and port
     - Check "Block common exploits"
   - Enable proxy mode in Cloudflare DNS settings.

6. **Install WordPress (optional):**

   - Refer to this tutorial for installing WordPress on Portainer: `How to install WordPress using Portainer on Oracle Cloud – Ubuntu 20.04 Arm64 server`

7. **Protect admin interfaces with NPM Access List:**

   - Create an access list rule in NPM:
     - Name it
     - Enable authorization
     - Set username and password
     - Choose optional conditions
   - Edit the desired host in NPM and apply the access list rule.


