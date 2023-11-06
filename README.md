# Tutorial: Configuração do NGINX Proxy Manager com Docker Swarm

Este tutorial fornece as etapas para configurar o [NGINX Proxy Manager](https://nginxproxymanager.com/guide/) utilizando Docker e Docker-Compose no modo Swarm.

## 1. Instalação do Docker e Docker-Compose

- **Docker**: Siga a [documentação de instalação do Docker](https://docs.docker.com/install/) para instalar o Docker em seu sistema.
- **Docker-Compose**: Após instalar o Docker, prossiga com a [instalação do Docker-Compose](https://docs.docker.com/compose/install/).

## 2. Configuração do Modo Swarm

Ative o modo Swarm com o seguinte comando:

```bash
docker swarm init
