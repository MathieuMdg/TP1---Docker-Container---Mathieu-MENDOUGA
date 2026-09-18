![alt text](image.png)

![alt text](image-1.png)

```bash
docker build -t simple-api .
```

```bash
docker run --rm --name simple-api --network app-network -p 8080:8080 simple-api
```

![alt text](image-2.png)

![alt text](image-3.png)