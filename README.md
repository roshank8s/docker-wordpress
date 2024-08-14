# Docker Compose Setup for WordPress with SSL

This repository contains a Docker Compose configuration for running a WordPress site with SSL support using Nginx and Let's Encrypt. The setup includes:

- **Nginx Proxy**: Handles HTTP and HTTPS traffic, acting as a reverse proxy.
- **Let's Encrypt**: Provides SSL certificates for secure HTTPS connections.
- **WordPress**: The popular CMS for managing content.
- **MySQL**: The database for WordPress.

## Requirements

- Docker
- Docker Compose

## Configuration

### Nginx Proxy

The `nginx-proxy` service listens on ports 80 and 443 and is responsible for routing traffic to the correct service based on the `VIRTUAL_HOST` environment variable. It also handles SSL termination.

### Let's Encrypt

The `letsencrypt` service automatically generates and renews SSL certificates using the Let's Encrypt API. It depends on the `nginx-proxy` service.

### WordPress

The `wordpress` service runs the latest WordPress image and connects to a MySQL database. It is configured to use the `nginx-proxy` and `letsencrypt` services for handling incoming traffic and securing connections.

### MySQL

The `db` service runs a MySQL instance used by WordPress for storing content.

## How to Use

1. **Clone the Repository**

   ```sh
   git clone https://github.com/yourusername/your-repo.git
   cd your-repo
2. **Update Configuration**

Update the docker-compose.yml file with your domain names and email addresses. Replace www.example.com and example@gmail.com with your own domain and email address.

3. **Start the Services**

docker-compose up -d

This command starts the services in detached mode.

4. **Access Your WordPress Site**

Navigate to https://www.example.com in your web browser. You should see the WordPress installation page if everything is set up correctly.

5. **Stopping and Removing Services**

To stop the services, run:

docker-compose down

This command stops and removes the containers but retains your data.

### Volumes
wordpress_data: Stores WordPress files and uploads.
db_data: Stores MySQL database files.
nginx_certs: Stores SSL certificates.
nginx_vhost: Stores Nginx virtual host configurations.
nginx_html: Stores Nginx HTML files.

### Notes
Ensure that your domain's DNS records point to your server's IP address.

The Let's Encrypt certificates are automatically renewed every 90 days.

If you encounter issues, check the logs of each service for troubleshooting:

docker-compose logs nginx-proxy
docker-compose logs letsencrypt
docker-compose logs wordpress
docker-compose logs db
