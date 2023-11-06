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
