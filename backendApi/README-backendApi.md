# Backend API

### Main.java

```java
public class Main {

   public static void main(String[] args) {
       System.out.println("Hello World!");
   }

}
```

### 1- Compile with your target Java: `javac Main.java`.

```bash
javac Main.java
```

![alt text](/backendApi/screenshots/screenshot-1.png)

![alt text](/backendApi/screenshots/screenshot-2.png)

### 2- Write dockerfile.

```dockerfile
FROM eclipse-temurin:25-jdk-alpine

COPY Main.class .

CMD ["java", "Main"]
```

### 3- Now, to launch app you have to do the same thing that Basic step 1.

```bash
docker build -t backend-api .
```

```bash
docker run --rm --name backend-api backend-api
```

![alt text](/backendApi/screenshots/screenshot-3.png)

### If it’s a success you must see “Hello Word” in your console.

![alt text](/backendApi/screenshots/screenshot-4.png)
