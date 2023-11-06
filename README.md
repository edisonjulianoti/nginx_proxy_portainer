# Configuração do NGINX Proxy Manager com Docker Swarm e Portainer

## Pré-requisitos
- Docker e Docker Compose instalados.

## Instalação e Configuração

1. **Instale Docker e Docker Compose:**
   - Docker: [Guia de Instalação](https://docs.docker.com/get-docker/)
   - Docker Compose: [Guia de Instalação](https://docs.docker.com/compose/install/)

2. **Inicialize o Docker Swarm:**
   Execute o comando para configurar seu Docker para o modo swarm:
   ```bash
   docker swarm init
   ```

## Portainer

1. **Crie um volume para o Portainer:**
   Crie um volume para armazenar os dados do Portainer com o comando:
   ```bash
   docker volume create portainer_data
   ```

2. **Execute o contêiner do Portainer:**
   Inicie o Portainer para gerenciar seus contêineres Docker:
   ```bash
   docker run -d -p 9000:9000 --name=portainer --restart=always \
   -v /var/run/docker.sock:/var/run/docker.sock \
   -v portainer_data:/data portainer/portainer-ce
   ```

## Docker Compose Yaml

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
      - '80:80'    # Public HTTP Port
      - '443:443'  # Public HTTPS Port
      - '81:81'    # Admin Web Port
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
      - rede_proxy

volumes: 
  npm_data:
    external: true
  npm_letsencrypt:
    external: true

networks:
  rede_proxy:
    external: true
```

## 3. Inicialização e Gerenciamento do Serviço

Inicie o NGINX Proxy Manager com o seguinte comando:
```bash
docker-compose up -d
```

## 4. Acesso ao NGINX Proxy Manager

Após a inicialização, acesse a interface de administração do NGINX Proxy Manager:
```
http://127.0.0.1:81
```
Utilize as credenciais padrão para o primeiro acesso e modifique-as conforme solicitado:
- Email: admin@example.com
- Senha: changeme
```
