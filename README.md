# SigNoz Deployment Directory (dokploy)

This directory contains optimized deployment configurations for SigNoz, focusing on high availability and simplified deployment.

## Directory Structure

- `common/`: Contains configuration files shared by all deployment methods
  - `clickhouse/`: ClickHouse database configuration files
  - `dashboards/`: SigNoz dashboard configurations
  - `signoz/`: SigNoz service configurations

- `docker/`: Docker Compose deployment configurations
  - `docker-compose.yaml`: Standard deployment configuration
  - `docker-compose.ha.yaml`: High availability deployment configuration
  - `otel-collector-config.yaml`: OpenTelemetry Collector configuration

## Deployment Features

1. **High Availability**: Provides basic high availability configuration, using up to two identical container instances
2. **Streamlined Configuration**: Only retains components and configurations necessary for deployment
3. **No Prometheus Dependency**: Removes Prometheus-related configurations, simplifying the deployment architecture
4. **Complete Documentation**: All configuration files include detailed comments for easy understanding and customization

## Deployment Methods

### Standard Deployment

```bash
cd dokploy/docker
docker-compose up -d
```

### High Availability Deployment

```bash
cd dokploy/docker
docker-compose -f docker-compose.ha.yaml up -d
```

## Environment Configuration

The deployment uses environment variables in the `.env` file for configuration. By default, it's configured for development environment:

```bash
# Default Development Environment
ENVIRONMENT=development  # 'development' or 'production'
LOG_LEVEL=debug         # 'debug', 'info', 'warn', 'error'
TELEMETRY_ENABLED=true  # Enable for more verbose logging
DEBUG=true              # Enable debug mode
```

### Production Environment
For production deployment, modify `.env` to:
```bash
ENVIRONMENT=production
LOG_LEVEL=info
TELEMETRY_ENABLED=false
DEBUG=false
```

## Notes

- Data is persistently stored in Docker volumes
- Default port configuration:
  - SigNoz UI: 8080
  - OpenTelemetry gRPC: 4317
  - OpenTelemetry HTTP: 4318
