# Express + Docker + NGINX

A minimal Node.js app containerized with Docker and served by an NGINX reverse proxy.

### 1. Build and Run

```sh
# Create a shared network
docker network create devops-net

# Build the app image
docker build -t express-app .

# Run the app and proxy containers
docker run -d --name express-app --network devops-net express-app
docker run -d --name nginx-proxy --network devops-net -p 80:80 -v $(pwd)/nginx.conf:/etc/nginx/nginx.conf:ro nginx
```

### 2. Verify

```sh
curl http://localhost
# Expected output: hello, devops!
```

### 3. Cleanup

```sh
docker stop express-app nginx-proxy
docker rm express-app nginx-proxy
docker network rm devops-net
```