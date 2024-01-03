# How to install WordPress using Portainer on Oracle Cloud – Ubuntu 20.04 | install WordPress on VPS hosting

## By Blog Edu Tech
## January 14, 2022

### Prerequisites:

    Create a VPS on Oracle Cloud
    Set up Virtual Cloud Network (VCN) to open required ports:
        SSH: 22
        HTTP: 80
        HTTPS: 443
        Portainer: 9000
        WordPress: 8181
    Log into the VPS using Putty
    Install Docker, Portainer, and Nginx Proxy Manager on the VPS

### Docker Compose configurations:

For non-ARM servers:
version: "3.9"

services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: somewordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress

  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    volumes:
      - wordpress_data:/var/www/html
    ports:
      - "8000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress

volumes:
  db_data: {}
  wordpress_data: {}
### For ARM servers:
version: "3.9"

services:
  db:
    image: lscr.io/linuxserver/mariadb
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: somewordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress

  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    volumes:
      - wordpress_data:/var/www/html
    ports:
      - "8000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress

volumes:
  db_data: {}
  wordpress_data: {}

### Deployment and configuration:

    Deploy the stack in Portainer.
    Access the WordPress installation wizard in a browser, but stop before completing it.
    Temporarily disable Cloudflare proxy and update IP address in DNS settings.
    Add a host in Nginx Proxy Manager, filling in details and updating IP and port.
    Click the domain to complete the WordPress installation.
    Re-enable Cloudflare proxy in DNS settings.
    Install and activate "Really Simple SSL" plugin in WordPress.
    Install "Flexible SSL for Cloudflare" plugin in WordPress.

### Additional notes:

    References:
        https://docs.docker.com/samples/wordpress/
        https://uk.sauber-lab.com/2021/11/16/lets-install-wordpress-on-docker-using-an-instance-on-oracle-cloud-ubuntu-20-04/
        https://hub.docker.com/r/mysql/mysql-server/
        https://hub.docker.com/_/wordpress
    For using free SSL with Cloudflare:
        Add domain to Cloudflare, choose "Flexible" and "Always use HTTPS."
        Update port in NPM.
        Enable proxy in Cloudflare DNS settings.
        Install and activate "Really Simple SSL" plugin in WordPress.
        WordPress Address (URL) and Site Address (URL) will automatically change to HTTPS.
