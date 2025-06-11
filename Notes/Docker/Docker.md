This is the place where I will store everything there is to know about Docker.


# Port Forwarding in Docker

Port forwarding in Docker refers to exposing ports from a container to the host machine, allowing external systems to communicate with services running inside the container.

---

Docker containers run in an isolated environment with their own network stack. By default, they cannot be accessed from outside unless ports are explicitly mapped.

When you run a container, you can specify port forwarding using the `-p` or `--publish` flag.

### **Basic Port Mapping Syntax**

```bash
docker run -p <host_port>:<container_port> <image_name>
```

- `<host_port>`: The port on the host machine (your computer or server).
- `<container_port>`: The port inside the container that the application is listening on.

---

## **2. How It Works**

When Docker starts a container with `-p`, it sets up **NAT (Network Address Translation)** rules to forward traffic from the host to the container.
Essentially *forwarding is done from host machine to the container.*
### **Example: Running a Web Server**

```bash
docker run -p 8080:80 nginx
```

- This maps **port 8080 on the host** to **port 80 inside the container**.
- Accessing `http://localhost:8080` on the host redirects to the Nginx server inside the container.

---

## **3. Checking Port Bindings**

To see which ports are mapped:

```bash
docker ps
```

It will show output like:

```
CONTAINER ID   IMAGE   PORTS                     NAMES
abcdef123456   nginx   0.0.0.0:8080->80/tcp      my-nginx
```

To inspect further:

```bash
docker inspect <container_id>
```

---

## **5. Common Issues & Troubleshooting**

1. **Port Already in Use**
    
    - If you get an error like:
        
        ```
        Error: port is already allocated
        ```
        
    - Another process is using that port. Check with:
        
        ```bash
        netstat -tulnp | grep 8080
        ```
        
    - Free up the port or use another one.
2. **Firewall Blocking the Port**
    
    - Ensure firewall rules allow traffic on the mapped port.
3. **Container Exposed Port**
    
    - Some images don't expose a port by default. Use:
        
        ```bash
        docker run -p 8080:5000 myapp
        ```
        
    - Ensure the app inside the container listens on the correct port.

---

## **6. Port Forwarding with Docker Compose**

If you are using **Docker Compose**, define ports in `docker-compose.yml`:

```yaml
services:
  web:
    image: nginx
    ports:
      - "8080:80"
```

Run it with:

```bash
docker-compose up -d
```

---

# Networking in Docker


Practice
1.[[Learning Docker Swarm]]