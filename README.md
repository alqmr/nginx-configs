# Nginx Configuration

Personal Nginx configuration for static website hosting with automated SSL/TLS.

## Overview

- HTTPS with Let's Encrypt
- HTTP to HTTPS redirection
- Gzip compression
- Static asset caching (30 days)
- Security hardening

## Structure
```
nginx.conf                     # Main configuration
sites-available/
  └── static-website.conf      # Site configuration
```

## Key Features

**Security:**
- Hidden Nginx version (`server_tokens off`)
- Block hidden files (`.git`, `.env`)
- Modern SSL/TLS configuration

**Performance:**
- Gzip compression for text assets
- Browser caching for static files
- Optimized file serving

## Deployment
```bash
# Install dependencies
apt install nginx certbot python3-certbot-nginx

# Copy configs
cp nginx.conf /etc/nginx/nginx.conf
cp sites-available/static-website.conf /etc/nginx/sites-available/

# Enable site
ln -s /etc/nginx/sites-available/static-website.conf /etc/nginx/sites-enabled/

# Test and reload
nginx -t
systemctl reload nginx

# Get SSL certificate
certbot --nginx -d example.com
```

## Configuration

Update these values in `static-website.conf`:
- `server_name`: your domain
- `root`: path to web files
- Log paths

## SSL Certificates

Certificates are managed by Certbot and renew automatically. 

Check status: `certbot certificates`

## Resources

- [Nginx docs](https://nginx.org/en/docs/)
- [Let's Encrypt](https://letsencrypt.org/)
