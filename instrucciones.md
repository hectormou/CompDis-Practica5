# Local

## Creacion de middlware RabbitMQ

```bash
docker run -d \
  --name middleware \
  --hostname container-host \
  -p 5672:5672 \
  -p 15672:15672 \
  --mount type=volume,source=COMPDISP5_RABBITMQ_DATA,target=/var/lib/rabbitmq \
  rabbitmq:4.4.0-management-alpine
```

## Creacion de DB

```bash
docker run -d \
  --name database \
  -e POSTGRES_PASSWORD=postgres \
  -p 5432:5432 \
  --mount type=volume,source=COMPDISP5_DB_DATA,target=/var/lib/postgresql/data \
  --mount type=bind,source="${PWD}/init-scripts/01-init.sql",target=/docker-entrypoint-initdb.d/init.sql:ro \
  postgres:18.6-alpine3.24
```

## Eliminar Container
Debemos para el container y luego borrarlo:
```bash
docker stop <container_name> && docker rm <container_name>
```

## Eliminar Volumenes

```bash
docker volume ls
docker volume rm <volume_name>
```

# Github CodeSpaces

## Inicializacion
Se hace automatica via /devcontainer/ . En este caso el script de iniciación se utiliza siempre que se abra el codespace.
Importante, los siguientes apartados solo aplican si se instala docker en el container en el que arranca vscode, si no no es posible.

## Resetear servicios

```bash
docker compose down
```

## Resetear todo

```bash
docker compose down -v
```
