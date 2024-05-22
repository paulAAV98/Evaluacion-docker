# DockerAngular

```
docker pull nginx:alpine
```

```
docker run -d -p 8080:80 nginx:alpine
```

```
docker ps
docker stop ID
```

```
ng new docker-angular
ng build --prod
```


```
docker run -d -p 8080:80 -v $(pwd)/dist/docker-angular:/usr/share/nginx/html nginx:alpine
```

Dockerfile v1
```
# Stage 0, based on Node.js, to build and compile Angular
FROM node:latest as node
WORKDIR /app
COPY ./ /app/
RUN npm install
RUN npm run build -- --prod

# Stage 1, based on Nginx, to have only the compiled app, ready for production with Nginx
FROM nginx:alpine
COPY --from=node /app/dist/docker-angular /usr/share/nginx/html
```

```
docker build .
docker build . -t docker-angular:latest
```

```
docker run -d -p 8080:80 docker-angular:latest
docker run -d -p 80:80 docker-angular:latest
```

```
ng build --prod --configuration=staging
```

```
# Stage 0, based on Node.js, to build and compile Angular
FROM node:latest as node
WORKDIR /app
COPY ./ /app/
RUN npm install
ARG configuration=production
RUN npm run build -- --prod --configuration=$configuration


```
