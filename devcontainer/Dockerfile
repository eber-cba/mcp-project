FROM mcr.microsoft.com/devcontainers/base:ubuntu

# Java & unzip
RUN apt-get update && \
    apt-get install -y openjdk-8-jdk unzip wget

# Instala Docker CLI (para docker-compose en Codespaces)
RUN apt-get install -y docker.io docker-compose

WORKDIR /workspace
``` :contentReference[oaicite:3]{index=3}  

---

## 3. Definir los servicios con Docker Compose

Crea `docker-compose.yml` en la raíz:

```yaml
version: '3.8'
services:
  mcp-dev:
    build:
      context: .
      dockerfile: .devcontainer/Dockerfile
    volumes:
      - ./:/workspace
    command: tail -f /dev/null

  postgres:
    image: postgres:14
    environment:
      POSTGRES_USER: mcpuser
      POSTGRES_PASSWORD: mcppass
      POSTGRES_DB: mcpdb
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data

  slack-cli:
    image: slackapi/slack-cli:latest
    entrypoint: ["tail", "-f", "/dev/null"]

volumes:
  pgdata:
