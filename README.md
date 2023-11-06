# Configuração do NGINX Proxy Manager com Docker Swarm e Portainer

## Pré-requisitos
- Docker e Docker Compose instalados.

## Instalação e Configuração
1. **Instale Docker e Docker Compose:**
   - Docker: [Guia de Instalação](https://docs.docker.com/get-docker/)
   - Docker Compose: [Guia de Instalação](https://docs.docker.com/compose/install/)

2. **Inicialize o Docker Swarm:**
   ```bash
   docker swarm init

## Portainer
1. **Crie um volume para o Portainer:**
    ```bash
    docker volume create portainer_data

2. **Execute o contêiner do Portainer:**
    ```bash
    docker run -d -p 9000:9000 --name=portainer --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data portainer/portainer-ce

## Configuração do NGINX Proxy Manager com Docker Swarm

```yaml
version: '3.8'

services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    volumes:
      - npm_data:/data
      - npm_letsencrypt:/etc/letsencrypt
    ports:
      - '80:80' # Public HTTP Port
      - '443:443' # Public HTTPS Port
      - '81:81' # Admin Web Port
    deploy:
      replicas: 1
      placement:
        constraints:
          - node.role == manager
      resources:
        limits:
          cpus: "0.1"
          memory: 256M
    networks:
      - npm_public

volumes: 
  npm_data:
    external: true
  npm_letsencrypt:
    external: true

networks:
  npm_public:
    external: true