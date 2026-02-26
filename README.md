# timescaledb-docker-scripts

## .env
```
HOST_PORT=5432

TIMESCALE_TAG=pg18
TIMESCALE_CONTAINER_NAME=timescale-container
TIMESCALE_VOLUME_NAME=timescale_volume

POSTGRES_DB=timescale
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres

VECTORIZER_WORKER_TAG=latest
VECTORIZER_WORKER_CONTAINER_NAME=vectorizer-worker-container
VECTORIZER_WORKER_POLL_INTERVAL=5s

OPENAI_BASE_URL=http://host.docker.internal:1234/v1
OPENAI_API_KEY=dummy
OPENAI_MODEL=text-embedding-qwen3-embedding-4b
```

## Step 1.
```bash
docker compose up -d timescaledb --force-recreate
```

## Step 2.
```bash
docker compose --profile worker up -d
```

## Step 3.
```bash
docker exec timescale-container curl http://host.docker.internal:1234/v1/models
```

## Step 4.
```bash
docker exec -it timescale-container psql -U postgres -d timescale
```

## Step 5.
```bash
SELECT extname, extversion FROM pg_extension WHERE extname IN ('ai', 'vectorscale', 'timescaledb');
```

### P.S.
```bash
docker compose down -v
```

```bash
docker logs timescale-container
```

```bash
docker logs vectorizer-worker-container
```
