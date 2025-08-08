# 🌐 FluffyChat Service

A modular Docker Compose configuration system for FluffyChat client with support for multiple environments. FluffyChat is a simple and modern Matrix client that provides a clean alternative to Element with fewer dependencies and a streamlined user experience.

## 🏗️ Project Structure

```sh
src/fluffychat/
├── components/                              # Source compose components
│   ├── base/                               # Base components
│   │   ├── docker-compose.yml              # Main FluffyChat service
│   │   └── .env.example                    # Base environment variables
│   ├── environments/                       # Environment components
│   │   ├── devcontainer/
│   │   │   └── docker-compose.yml          # DevContainer environment
│   │   ├── forwarding/
│   │   │   └── docker-compose.yml          # Development with port forwarding
│   │   ├── letsencrypt/
│   │   │   ├── docker-compose.yml          # Let's Encrypt SSL
│   │   │   └── .env.example                # Let's Encrypt variables
│   │   └── step-ca/
│   │       ├── docker-compose.yml          # Step CA SSL
│   │       └── .env.example                # Step CA variables
│   └── extensions/                         # Extension components (optional)
├── build/                        # Generated configurations (auto-generated)
│   ├── devcontainer/
│   │   └── base/                 # DevContainer + base
│   ├── forwarding/
│   │   └── base/                 # Development + base
│   ├── letsencrypt/
│   │   └── base/                 # Let's Encrypt + base
│   └── step-ca/
│       └── base/                 # Step CA + base
├── build.sh                      # Build script
└── README.md                     # This file
```

## 🚀 Quick Start

### 1. Build Configurations

Run the build script to generate all possible combinations:

```bash
./build.sh
```

This will create all combinations in the `build/` directory.

### 2. Choose Your Configuration

Navigate to the desired configuration directory:

```bash
# For development with port forwarding
cd build/forwarding/base/

# For DevContainer environment
cd build/devcontainer/base/

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
docker-compose up -d
```

Access: `http://localhost:3000` (for forwarding mode)

## 🔧 Available Configurations

### Environments

- **devcontainer**: Development environment with workspace network
- **forwarding**: Development environment with port forwarding (3000:80)
- **letsencrypt**: Production with Let's Encrypt SSL certificates
- **step-ca**: Production with Step CA SSL certificates

### Generated Combinations

Each environment provides a complete FluffyChat deployment:

**Base configurations:**

- `devcontainer/base` - DevContainer development setup
- `forwarding/base` - Development with port forwarding
- `letsencrypt/base` - Production with Let's Encrypt SSL
- `step-ca/base` - Production with Step CA SSL

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

## 🛠️ Development

### Adding New Environments

1. Create directory in `components/environments/` with `docker-compose.yml` and optional `.env.example` file
2. Run `./build.sh` to generate new combinations

### Adding New Extensions

1. Create directory in `components/extensions/` with `docker-compose.yml` and optional `.env.example` file
2. Run `./build.sh` to generate new combinations with all environments
3. Extensions are automatically combined with all available environments

### File Naming Convention

All component files follow the standard Docker Compose naming convention (`docker-compose.yml`) for:

- **VS Code compatibility**: Full support for Docker Compose language features and IntelliSense
- **IDE integration**: Proper syntax highlighting and validation in all major editors
- **Tool compatibility**: Works with Docker Compose plugins and extensions
- **Standard compliance**: Follows official Docker Compose file naming patterns

### Modifying Existing Components

1. Edit the component files in `components/`
2. Run `./build.sh` to regenerate configurations
3. The `build/` directory will be completely recreated

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

- Ensure `yq` is installed: <https://github.com/mikefarah/yq#install>
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

- The `build/` directory is automatically generated and should not be edited manually
- Environment variables in generated files use `$VARIABLE_NAME` format for proper interpolation
- Each generated configuration includes a complete `docker-compose.yml` and `.env.example`
- Missing `.env.*` files for components are handled gracefully by the build script
- FluffyChat requires proper Matrix homeserver configuration for functionality

## 🔄 Configuration Management

The build system automatically:

- Merges base and environment configurations
- Copies additional files and configurations
- Generates complete deployment configurations
- Preserves user `.env` files during rebuilds

**Build approach:**

```bash
./build.sh
cd build/forwarding/base/
cp .env.example .env
# Edit .env with your values
docker-compose up -d
```

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
