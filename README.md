# WordPress Alpine Docker Setup

A lightweight WordPress development environment using Alpine Linux containers with Nginx, PHP-FPM, and MariaDB.

## Features

- **Nginx Alpine**: Fast and lightweight web server
- **WordPress PHP 8.4 FPM Alpine**: Latest PHP with FPM for better performance
- **MariaDB 11**: Modern MySQL-compatible database
- **Docker Compose**: Easy container orchestration

## Quick Start

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd wp-alpine
   ```

2. **Set up environment variables**
   ```bash
   cp env.example .env
   ```
   Edit `.env` and set your database passwords.

3. **Start the containers**
   ```bash
   docker-compose up -d
   ```

4. **Access WordPress**
   Open your browser and go to `http://localhost:8080`

## Configuration

### Environment Variables

Copy `env.example` to `.env` and configure:

- `SERVICE_USER_WORDPRESS`: Database user for WordPress
- `SERVICE_PASSWORD_WORDPRESS`: Password for WordPress database user
- `SERVICE_PASSWORD_ROOT`: Root password for MariaDB

### Nginx Configuration

The `nginx.conf` file contains the web server configuration with:
- PHP-FPM integration
- WordPress-friendly URL rewriting
- Security headers

## Services

- **WordPress**: Available at `http://localhost:8080`
- **Nginx**: Port 8080 (mapped to container port 80)
- **MariaDB**: Internal container communication only

## Volumes

- `wordpress-files`: Persistent WordPress files
- `mariadb-data`: Persistent database storage

## Development

To view logs:
```bash
docker-compose logs -f
```

To stop services:
```bash
docker-compose down
```

To rebuild containers:
```bash
docker-compose up --build
```

## Security Notes

- Change default passwords in `.env` file
- Consider using SSL/TLS for production deployments
- Regularly update container images

## Coolify Deployment

This project is optimized for deployment on [Coolify](https://coolify.io/), a self-hosted alternative to Heroku.

### Quick Coolify Setup

1. **Use the Coolify configuration**:
   - Use `docker-compose.coolify.yml` instead of `docker-compose.yml`
   - Copy `coolify.env.example` to `.env` and configure your domain

2. **Required Environment Variables**:
   ```env
   DOMAIN=yourdomain.com
   SERVICE_USER_WORDPRESS=wordpress_user
   SERVICE_PASSWORD_WORDPRESS=your_secure_password
   SERVICE_PASSWORD_ROOT=your_secure_root_password
   ```

3. **Deploy on Coolify**:
   - Connect your GitHub repository
   - Select Docker Compose build pack
   - Use `docker-compose.coolify.yml` as your compose file
   - Set your environment variables

For detailed deployment instructions, see [COOLIFY-DEPLOYMENT.md](COOLIFY-DEPLOYMENT.md).

### Coolify Features

- **Automatic SSL**: Let's Encrypt certificates via Traefik
- **Health Checks**: Container monitoring and auto-restart
- **Domain Management**: Easy domain configuration
- **Zero-Downtime Deployments**: Rolling updates

## License

This project is open source and available under the [MIT License](LICENSE).
