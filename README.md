# Outline Wiki Setup

This repository contains the Docker configuration for running a self-hosted instance of Outline Wiki, a modern team knowledge base and documentation platform.

## Project Structure

```
outline/
├── docker-compose.yml    # Docker services configuration
├── docker.env           # Environment variables
├── redis.conf/         # Redis configuration
└── volumes/            # Persistent storage
    ├── database-data/  # PostgreSQL data
    └── storage-data/   # Document attachments and images
```

## Services

The setup includes three main services:

1. **Outline Application**
   - Port: 3000
   - Main application interface
   - Handles document management and user interactions

2. **PostgreSQL Database**
   - Port: 5432
   - Stores document content and metadata
   - Persistent storage in `database-data` volume

3. **Redis**
   - Port: 6379
   - Handles caching and real-time collaboration
   - Uses custom configuration from `redis.conf`

## Authentication

The system is configured with Google OAuth authentication:
- Redirect URI: http://localhost:3000/auth/google.callback
- Google Cloud Console configuration required

## Storage

Documents and data are stored in two locations:

1. **PostgreSQL Database**
   - Document content
   - User information
   - Metadata
   - Stored in persistent volume: `database-data`

2. **Local File Storage**
   - Attachments and images
   - Storage path: `/var/lib/outline/data`
   - Stored in persistent volume: `storage-data`

## Environment Configuration

Key configurations in `docker.env`:
- Database connection settings
- Redis connection settings
- Google OAuth credentials
- File storage settings
- Security keys

## Getting Started

1. Clone this repository
2. Configure Google OAuth credentials in `docker.env`
3. Start the services:
   ```bash
   docker compose up -d
   ```
4. Access Outline at http://localhost:3000

## Maintenance

- Backup the PostgreSQL database regularly
- Monitor the storage volumes
- Keep track of log files for troubleshooting

## Security Notes

- All sensitive credentials are stored in `docker.env`
- SSL/TLS termination should be handled by a reverse proxy in production
- Regular security updates are recommended

## Additional Resources

- [Outline Official Documentation](https://docs.getoutline.com/)
- [Docker Documentation](https://docs.docker.com/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/) 