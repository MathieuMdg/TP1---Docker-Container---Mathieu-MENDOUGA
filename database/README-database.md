# Database

## Basics

We use the image: postgres:17.2-alpine.

### Dockerfile

```dockerfile
FROM postgres:17.2-alpine

COPY CreateScheme.sql /docker-entrypoint-initdb.d/01-create-scheme.sql
COPY InsertData.sql /docker-entrypoint-initdb.d/02-insert-data.sql
```

![alt text](/database/screenshots/screenshot-1.png)

### Build this image and start a container properly.

```bash
docker build -t postgres-server .
```

```bash
docker run -d --name server --network app-network postgres-server
```

![alt text](/database/screenshots/screenshot-2.png)

## Adminer

### Re-run your database with adminer.

```bash
docker network create app-network
```

```bash
docker run -d --name adminerapp --network app-network -p 8090:8080 adminer
```
![alt text](/database/screenshots/screenshot-3.png)

---

## Init database

### 01-CreateScheme.sql

![alt text](/database/screenshots/screenshot-4.png)

### 02-InsertData.sql

![alt text](/database/screenshots/screenshot-5.png)

### Rebuild your image and check that your scripts have been executed at startup and that the data is present in your container.

```bash
docker build -t postgres-db-container .
```

![alt text](/database/screenshots/screenshot-6.png)

![alt text](/database/screenshots/screenshot-7.png)

---

## Persist data

### Use volumes to persist data on the host disk.

![alt text](/database/screenshots/screenshot-8.png)

![alt text](/database/screenshots/screenshot-9.png)

---

## Questions

### 1-1 For which reason is it better to run the container with a flag `-e` to give the environment variables rather than put them directly in the Dockerfile?

Because sensitive information such as database passwords should not be stored directly in the Dockerfile.

### 1-2 Why do we need a volume to be attached to our postgres container?

If the PostgreSQL container is removed, the data stored inside the container is lost. A volume provides persistent storage outside the container.

### 1-3 Document your database container essentials: commands and Dockerfile.

Dockerfile : 
    FROM postgres:17.2-alpine

    COPY init/ /docker-entrypoint-initdb.d/


Build :
```bash
docker build -t postgres-server .
```

```bash
docker run -d --name server --network app-network postgres-server
```

Network :
```bash
docker network create app-network
```

Adminer :
```bash
docker run -d --name adminerapp --network app-network -p 8090:8080 adminer
```

