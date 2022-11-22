# Build image

1. Do not use base operating system image, Install packages by yourself
    ```docker
    FROM ubuntu 
    
    RUN apt-get update ...
    ```
    
    Do use offical image
    
    ```docker
    FROM node
    ```
    
    - cleaner Dockerfile
    - official Docker image
    - verified and already built best practices

2. Do not latest tag
    ```docker
    FROM node:latest
    ```
    
    - difference docker image version
    - break stuff
    - unpredictable
    
    Fixate version
    
    ```docker
    FROM node:17.0.1
    ```
    
3. Use smaller image
    - less space storage
    - transfer image faster
    - safe security
    - minimize attac surfaces
    
    ```docker
    FROM node:17.0.1-alpine
    ```
    
4. Optimize Caching image layer
    ```docker
    FROM node
    
    WORKDIR /app
    
    COPY package.json /app/package.json
    
    RUN npm install --production
    
    COPY myapp /app
    
    CMD ["node", "src/index.js"]
    ```
    
5. Do not include unnecessary files → Use .dockerignore
    - README
    - env, secret
    - ide
    - dockerfile

6. Multi stage builds 
    ```docker
    # syntax=docker/dockerfile:1
    FROM golang:1.16
    WORKDIR /go/src/github.com/alexellis/href-counter/
    RUN go get -d -v golang.org/x/net/html  
    COPY app.go ./
    RUN CGO_ENABLED=0 go build -a -installsuffix cgo -o app .

    FROM alpine:latest  
    RUN apk --no-cache add ca-certificates
    WORKDIR /root/
    COPY --from=0 /go/src/github.com/alexellis/href-counter/app ./
    CMD ["./app"]
    ```
    
7. Do not root user
    ```docker
    RUN groupadd -r tom && useradd -g tom tom
    
    RUN chown -R tom:tom /app

    USER tom

    CMD node index.js
    ```
    
8. Do scan docker image for detect vulnerability
    docker scan myapp:1.0