# 🌐 FluffyChat Service

A modular Docker Compose configuration system for FluffyChat client with support for multiple environments. FluffyChat is a simple and modern Matrix client that provides a clean alternative to Element with fewer dependencies and a streamlined user experience.

## 🚀 Quick Start

### 1. Build Configurations

Use the stackbuilder utility to generate all configurations:

```bash
sb build
```

This creates ready-to-deploy Docker Compose files in the `build/` directory.

### 2. Choose Your Configuration

Navigate to the desired configuration directory:

```bash
# For development with port forwarding
cd build/forwarding/base/

# For production with Let's Encrypt SSL
cd build/letsencrypt/base/

# For production with Step CA SSL
cd build/step-ca/base/
```

### 3. Configure Environment

Copy and edit the environment file:

```bash
cp .env.example .env
# Edit .env with your values
```

### 4. Deploy

Start the services:

```bash
docker compose up --build -d
```

Access: `http://localhost:3000` (for forwarding mode)

## 🔧 Available Environments

- **forwarding**: Development environment with port forwarding (3000:80)
- **letsencrypt**: Production with Let's Encrypt SSL certificates
- **step-ca**: Production with Step CA SSL certificates

## 🔧 Environment Variables

### Base Configuration

- `COMPOSE_PROJECT_NAME`: Project name for Docker Compose (default: fluffychat)

### Let's Encrypt Configuration

- `VIRTUAL_PORT`: Port for nginx-proxy (default: 80)
- `VIRTUAL_HOST`: Domain for nginx-proxy (e.g., fluffychat.example.com)
- `LETSENCRYPT_HOST`: Domain for SSL certificate
- `LETSENCRYPT_EMAIL`: Email for certificate registration

### Step CA Configuration

- `VIRTUAL_PORT`: Port for nginx-proxy (default: 80)
- `VIRTUAL_HOST`: Domain for nginx-proxy (e.g., fluffychat.local)
- `LETSENCRYPT_HOST`: Domain for SSL certificate
- `LETSENCRYPT_EMAIL`: Email for certificate registration

## 🌐 Networks

- **Development**: `fluffychat-network` (internal)
- **DevContainer**: `fluffychat-workspace-network` (external)
- **Let's Encrypt**: `letsencrypt-network` (external)
- **Step CA**: `step-ca-network` (external)

## 🔒 Security

⚠️ **Production Checklist:**

- Configure proper Matrix homeserver URL
- Set up proper firewall rules
- Regular security updates
- Configure rate limiting
- Set up proper logging
- Validate SSL certificates

## 🆘 Troubleshooting

**Build Issues:**

- Ensure `sb` (stackbuilder) is installed: <https://github.com/zyrakq/stackbuilder>
- Check component file syntax
- Verify all required files exist

**FluffyChat Issues:**

- Verify Matrix homeserver connection
- Review container logs: `docker logs fluffychat`
- Check network connectivity

**SSL Issues:**

- **Let's Encrypt**: Verify domain DNS and letsencrypt-manager
- **Step CA**: Check step-ca-manager and virtual network config

**Matrix Connection Issues:**

- Verify Matrix homeserver is accessible
- Check CORS configuration on homeserver
- Validate SSL certificates
- Check network connectivity between FluffyChat and Matrix

## 📝 Notes

- The `build/` directory contains auto-generated Docker Compose configurations
- Environment variables in generated files use `$VARIABLE_NAME` format for proper interpolation
- Each generated configuration includes a complete `docker-compose.yml` and `.env.example`
- FluffyChat requires proper Matrix homeserver configuration for functionality
- Source components are in the `components/` directory and are built into final configurations using `sb build`

## 🎨 FluffyChat Features

The FluffyChat configuration includes:

- **Simple UI**: Clean and intuitive interface
- **Cross-platform**: Works on web, mobile, and desktop
- **Lightweight**: Minimal resource usage
- **Modern Design**: Material Design 3 interface
- **Fast Performance**: Optimized for speed
- **Privacy-focused**: No tracking or analytics
- **Open Source**: Fully open source Matrix client
- **Easy Setup**: Simple configuration and deployment

## ⚙️ Advanced Configuration

For detailed configuration options of FluffyChat, including customization and Matrix homeserver setup, see the official FluffyChat documentation:

📖 **[FluffyChat Documentation](https://docs.fluffychat.im/)**

This comprehensive guide covers:

- Homeserver configuration options
- Customization settings
- Deployment configurations
- Troubleshooting guides

## 🔗 Integration

FluffyChat works seamlessly with:

- **Matrix Synapse**: Primary Matrix homeserver
- **Dendrite**: Lightweight Matrix homeserver
- **Conduit**: Fast Matrix homeserver written in Rust
- **Custom Homeservers**: Any Matrix-compatible server

## 🌟 Why FluffyChat?

FluffyChat offers several advantages over Element:

- **Simplicity**: Cleaner, more intuitive interface
- **Performance**: Faster loading and better resource usage
- **Lightweight**: Smaller footprint and fewer dependencies
- **Modern**: Built with modern technologies and design principles
- **Privacy**: No tracking, analytics, or telemetry
- **Open Source**: Fully transparent and community-driven
