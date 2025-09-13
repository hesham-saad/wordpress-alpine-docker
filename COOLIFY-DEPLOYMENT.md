# Coolify Deployment Guide

This guide will help you deploy your WordPress Alpine Docker project on Coolify.

## Prerequisites

- A server with Coolify installed
- A domain name pointing to your server
- GitHub repository access

## Step 1: Install Coolify

If you haven't installed Coolify yet, run this command on your server:

```bash
curl -fsSL https://cdn.coollabs.io/coolify/install.sh | bash
```

Coolify will be available at `http://your-server-ip:8000`

## Step 2: Connect GitHub Repository

1. **Access Coolify Dashboard**
   - Open your browser and go to `http://your-server-ip:8000`
   - Complete the initial setup

2. **Add GitHub Integration**
   - Go to **Settings** → **Source Providers**
   - Click **Add GitHub**
   - Authorize Coolify to access your repositories

3. **Create New Project**
   - Go to **Projects** → **Add New Project**
   - Select **GitHub** as source
   - Choose your `wordpress-alpine-docker` repository

## Step 3: Configure Deployment

1. **Select Build Pack**
   - Choose **Docker Compose** as the build pack

2. **Configure Repository Settings**
   - **Branch**: `main`
   - **Docker Compose File**: `docker-compose.coolify.yml`
   - **Environment File**: `.env` (you'll create this)

3. **Set Environment Variables**
   Create a `.env` file in your repository root with these variables:

   ```env
   # Required
   DOMAIN=yourdomain.com
   SERVICE_USER_WORDPRESS=wordpress_user
   SERVICE_PASSWORD_WORDPRESS=your_secure_password
   SERVICE_PASSWORD_ROOT=your_secure_root_password
   ```

   **Important**: Replace `yourdomain.com` with your actual domain name.

## Step 4: Deploy

1. **Start Deployment**
   - Click **Deploy** in the Coolify dashboard
   - Monitor the build logs for any issues

2. **Wait for Deployment**
   - The deployment process will:
     - Pull your repository
     - Build the Docker containers
     - Start all services
     - Configure SSL certificates (if domain is set)

## Step 5: Access Your WordPress Site

1. **Get Your URL**
   - Once deployed, Coolify will provide a URL
   - It will be something like: `https://yourdomain.com`

2. **Complete WordPress Setup**
   - Visit your domain
   - Follow the WordPress installation wizard
   - Create your admin account

## Configuration Files

### For Coolify Deployment
- `docker-compose.coolify.yml` - Coolify-optimized Docker Compose
- `coolify.env.example` - Environment variables template

### Key Differences from Local Development
- **Traefik Integration**: Automatic SSL certificates and reverse proxy
- **Health Checks**: Container health monitoring
- **Domain Configuration**: WordPress configured for your domain
- **SSL Enforcement**: HTTPS redirects and secure admin

## Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `DOMAIN` | Your domain name | Yes |
| `SERVICE_USER_WORDPRESS` | WordPress database user | Yes |
| `SERVICE_PASSWORD_WORDPRESS` | WordPress database password | Yes |
| `SERVICE_PASSWORD_ROOT` | MariaDB root password | Yes |

## Troubleshooting

### Common Issues

1. **Domain Not Working**
   - Ensure DNS records point to your server
   - Check that `DOMAIN` environment variable is set correctly

2. **SSL Certificate Issues**
   - Verify domain is accessible via HTTP first
   - Check Traefik logs in Coolify dashboard

3. **Database Connection Issues**
   - Verify environment variables are set correctly
   - Check MariaDB container logs

4. **WordPress Not Loading**
   - Check Nginx container logs
   - Verify file permissions in WordPress volume

### Logs and Monitoring

- **Application Logs**: Available in Coolify dashboard
- **Container Logs**: Click on individual services to view logs
- **Health Checks**: Monitor service health in the dashboard

## Security Considerations

1. **Strong Passwords**: Use complex passwords for database users
2. **Regular Updates**: Keep WordPress and plugins updated
3. **Backup Strategy**: Set up regular database and file backups
4. **Firewall**: Configure server firewall appropriately

## Scaling and Performance

- **Resource Limits**: Set appropriate CPU/memory limits in Coolify
- **Caching**: Consider adding Redis for object caching
- **CDN**: Use a CDN for static assets
- **Database Optimization**: Monitor database performance

## Support

- **Coolify Documentation**: [https://coolify.io/docs](https://coolify.io/docs)
- **WordPress Documentation**: [https://wordpress.org/support/](https://wordpress.org/support/)
- **Docker Documentation**: [https://docs.docker.com/](https://docs.docker.com/)

## Next Steps

After successful deployment:

1. **Configure WordPress**: Set up themes, plugins, and content
2. **Set Up Backups**: Implement automated backup strategy
3. **Monitor Performance**: Use Coolify's monitoring features
4. **Security Hardening**: Apply WordPress security best practices
