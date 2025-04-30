# n8n Docker Setup with Caddy and PostgreSQL

This repository contains a Docker setup for running n8n with Caddy as a reverse proxy and PostgreSQL as the database.

## Overview

This setup includes:
- n8n: Workflow automation tool
- Caddy: Modern web server and reverse proxy
- PostgreSQL: Database for storing n8n data

## Prerequisites

- Docker
- Docker Compose
- Basic understanding of Docker and networking

## Getting Started

1. Clone this repository:
```bash
git clone https://github.com/WestOakWebDesigns/n8n-docker-caddy-postgres
cd n8n-docker
```

2. Create a `.env` file with the following variables:
```env
POSTGRES_USER=n8n
POSTGRES_PASSWORD=your_secure_password
POSTGRES_DB=n8n
POSTGRES_NON_ROOT_USER=n8n
POSTGRES_NON_ROOT_PASSWORD=your_secure_password
POSTGRES_HOST=postgres
POSTGRES_PORT=5432

N8N_HOST=your-domain.com
N8N_PROTOCOL=https
N8N_PORT=5678
N8N_ENCRYPTION_KEY=your_secure_encryption_key
```

3. Start the services:
```bash
docker-compose up -d
```

## Directory Structure

├── docker-compose.yml
├── Caddyfile
├── .env
└── README.md

## Configuration

### n8n
- The n8n instance will be available at `https://your-domain.com`
- Default port: 5678
- Persistence is enabled by default using PostgreSQL

### Caddy
- Acts as a reverse proxy
- Handles SSL/TLS certificate automation
- Provides secure access to n8n

### PostgreSQL
- Runs on default port 5432
- Data is persisted using Docker volumes
- Includes secure user configuration


## Security Considerations

1. Always change default passwords in the `.env` file
2. Use strong passwords for PostgreSQL
3. Set a secure encryption key for n8n
4. Keep your Docker images updated

## Maintenance

### Updating n8n

To update n8n to the latest version:

```bash
docker-compose pull
docker-compose up -d
```

### Backup

To backup the PostgreSQL database:

```bash
docker-compose exec postgres pg_dump -U n8n n8n > backup.sql
```

## Troubleshooting

### Common Issues

1. If n8n can't connect to PostgreSQL:
   - Check if PostgreSQL container is running
   - Verify database credentials in `.env`
   - Ensure proper network connectivity between containers

2. If Caddy fails to start:
   - Check if ports 80 and 443 are available
   - Verify domain configuration in Caddyfile
   - Ensure proper permissions for SSL certificate storage

## Contributing

This is a fork of the official [n8n-docker-caddy](https://github.com/n8n-io/n8n-docker-caddy) repository. Feel free to submit issues and enhancement requests to this fork for PostgreSQL-specific configurations. For core n8n-docker-caddy issues, please refer to the original repository.

## Credits

This project is based on the official [n8n-docker-caddy](https://github.com/n8n-io/n8n-docker-caddy) repository by the n8n team. The original project is designed to get n8n up and running on various platforms including DigitalOcean and Hetzner Cloud.


## Support

For support:
- n8n Documentation: https://docs.n8n.io/
- Caddy Documentation: https://caddyserver.com/docs/
- PostgreSQL Documentation: https://www.postgresql.org/docs/
- Original n8n-docker-caddy Repository: https://github.com/n8n-io/n8n-docker-caddy