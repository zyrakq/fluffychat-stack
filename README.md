# 🌐 FluffyChat Stack

Complete Docker-based FluffyChat deployment with SSL certificate management for production and development environments. FluffyChat is a simple and modern Matrix client that provides a clean alternative to Element with fewer dependencies and a streamlined user experience.

## 🧩 Components

### 🔐 SSL Automation

#### [🔒 Let's Encrypt Manager](src/ssl-automation/letsencrypt-manager)

Automatic SSL certificate management from Let's Encrypt for production deployments. Provides seamless HTTPS integration for Docker containers using nginx-proxy and acme-companion.
[Learn more about Let's Encrypt Manager configuration](src/ssl-automation/letsencrypt-manager/README.md).

#### [🏠 Step CA Manager](src/ssl-automation/step-ca-manager)

Local domain stack with trusted self-signed certificates for virtual network deployments. Includes private CA management and local DNS resolution for development environments.
[Learn more about Step CA Manager configuration](src/ssl-automation/step-ca-manager/README.md).

### 💬 Matrix Services

#### [🏠 Synapse](src/matrix/synapse)

Matrix homeserver implementation providing the backend infrastructure for FluffyChat client. Includes PostgreSQL backend and multiple deployment configurations.
[Learn more about Matrix Synapse configuration](src/matrix/synapse/README.md).

## 🌐 Services

### 🌐 [FluffyChat](src/fluffychat/)

Modular Docker Compose configuration system for FluffyChat client with support for multiple environments. Provides complete Matrix web client deployment with customizable configurations for development and production.
[Learn more about FluffyChat configuration](src/fluffychat/README.md).

## 🚀 Quick Start

Each component has its own README with detailed setup instructions. Choose the certificate management solution that fits your deployment scenario.

### Basic Setup

1. **Choose SSL Management:**
   - Production: Use Let's Encrypt Manager
   - Development: Use Step CA Manager

2. **Deploy Matrix Backend:**
   - Set up Synapse homeserver

3. **Deploy FluffyChat:**
   - Configure FluffyChat client to connect to your Matrix homeserver

## 🏗️ Architecture

```sh
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   FluffyChat    │────│  Matrix Synapse │────│   PostgreSQL    │
│   (Frontend)    │    │   (Homeserver)  │    │   (Database)    │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │
         │                       │
┌─────────────────┐
│  SSL Manager    │
│ (Let's Encrypt/ │
│  Step CA)       │
└─────────────────┘
```

## 📋 Requirements

- Docker & Docker Compose
- Domain name (for production deployments)
- Email address (for Let's Encrypt)
- `yq` tool for configuration building

## 🔧 Configuration

All services use modular Docker Compose configurations with:

- **Base components**: Core service definitions
- **Environment components**: Development, production, SSL configurations
- **Build system**: Automatic generation of deployment combinations

## 🌍 Deployment Scenarios

### Development Environment

```bash
# FluffyChat with port forwarding
cd src/fluffychat/build/forwarding/base/
docker-compose up -d

# Synapse with port forwarding
cd src/matrix/synapse/build/forwarding/base/
docker-compose up -d
```

### Production Environment

```bash
# FluffyChat with Let's Encrypt SSL
cd src/fluffychat/build/letsencrypt/base/
docker-compose up -d

# Synapse with Let's Encrypt SSL
cd src/matrix/synapse/build/letsencrypt/base/
docker-compose up -d
```

### DevContainer Environment

```bash
# FluffyChat in DevContainer
cd src/fluffychat/build/devcontainer/base/
docker-compose up -d

# Synapse in DevContainer
cd src/matrix/synapse/build/devcontainer/base/
docker-compose up -d
```

## 🔐 Security Features

- **SSL/TLS Encryption**: Automatic certificate management
- **Network Isolation**: Docker network segmentation
- **Secret Management**: Environment-based configuration
- **Access Control**: Matrix-based permissions

## 🆘 Troubleshooting

### Common Issues

- **SSL Certificate Issues**: Check Let's Encrypt/Step CA configuration
- **Network Connectivity**: Ensure proper Docker network configuration
- **Database Connection**: Check PostgreSQL connectivity for Synapse

### Logs

```bash
# FluffyChat logs
docker logs fluffychat

# Synapse logs
docker logs matrix
```

## 📚 Documentation

- [FluffyChat Configuration](src/fluffychat/README.md)
- [Matrix Synapse Setup](src/matrix/synapse/README.md)
- [SSL Automation](src/ssl-automation/)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test configurations
5. Submit a pull request

## 📄 License

This project is dual-licensed under:

- [Apache License 2.0](LICENSE-APACHE)
- [MIT License](LICENSE-MIT)

## 🔗 Related Projects

- [Matrix.org](https://matrix.org/) - Open network for secure, decentralized communication
- [FluffyChat](https://fluffychat.im/) - Simple and modern Matrix client
- [Synapse](https://github.com/matrix-org/synapse) - Matrix homeserver implementation
