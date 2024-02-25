# Prácticas de GPG con Docker

Este repositorio contiene un entorno Docker configurado con las herramientas necesarias para practicar con GPG (GNU Privacy Guard).

## Iniciar el contenedor Docker

Utilizaremos Docker Compose para iniciar el contenedor. Ejecuta el siguiente comando:

```bash
 docker compose up -d --build
```

## Conectarse al contenedor A

```bash
docker-compose exec gpg-container-a bash
```

## Conectarse al contenedor B

```bash
docker-compose exec gpg-container-b bash
```

## Detener el contenedor

```bash
docker-compose down
```
