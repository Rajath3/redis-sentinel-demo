# Redis Sentinel Demo

This project demonstrates high availability Redis setup using Redis Sentinel.

## Prerequisites

- Docker
- Docker Compose

## Project Structure

```
redis-sentinel-demo/
├── docker compose.yml
└── README.md
```

## Quick Start

1. Start the Redis cluster:
```bash
docker compose up -d
```

2. Verify the containers:
```bash
docker compose ps
```

## Architecture

- 1 Redis master
- 2 Redis replicas
- 3 Sentinel nodes

## Testing Failover

1. Connect to Redis master:
```bash
docker exec -it redis-master redis-cli
```

2. Simulate master failure:
```bash
docker stop redis-master
```

3. Check new master:
```bash
docker exec -it sentinel-1 redis-cli -p 26379 sentinel get-master-addr-by-name mymaster
```

4. Monitor failover process:
```bash
docker compose logs -f sentinel-1 sentinel-2 sentinel-3
```

5. Verify replica promotion: It should be either redis-replica-1 or redis-replica-2
```bash
docker exec -it redis-replica-1 redis-cli info replication
```

## Shutdown

```bash
docker compose down
```

## Monitoring

View Sentinel logs:
```bash
docker compose logs sentinel-1
```
