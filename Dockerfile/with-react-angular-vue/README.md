# Static Application Deployment with Docker and Nginx (with React, Angular, Vue)

This project is a template for deploying static applications with Docker and Nginx. It is intended to be used as a starting point for deploying React, Angular, or Vue applications.

## Table of Contents

1. [Installation](#installation)
2. [Usage](#usage)
3. [Explanation](#explanation)
   1. [Dockerfile](#dockerfile)
   2. [nginx.conf](#nginxconf)
4. [Contributing](#contributing)
5. [License](#license)

<a id="installation"></a>

## 1. Installation

Clone the repository. You can run `npm install` to install the dependencies and `npn run dev` to start the development server.

Requirements:

- Docker
- Node.js

<a id="usage"></a>

## 2. Usage

```bash
# Build the image
docker build -t <image-name> .

# Run the container
docker run -d -p <host-port>:80 <image-name>
```

<a id="explanation"></a>

## 3. Explanation

<a id="dockerfile"></a>

### 3.1. Dockerfile

```dockerfile
# Multi-stage build
# https://docs.docker.com/develop/develop-images/multistage-build/

# Build stage
FROM node:20-alpine as build-stage # Use node:alpine as base image
WORKDIR /app # Set working directory
COPY package*.json ./ # Copy package.json and package-lock.json
RUN npm ci && npm cache clean --force # Install dependencies
COPY . .
RUN npm run build # Build application

# Production stage
FROM nginx:stable-alpine as production-stage # Use nginx:alpine as base image
COPY nginx.conf /etc/nginx/conf.d/default.conf # Copy nginx configuration
WORKDIR /usr/share/nginx/html # Set working directory
RUN rm -rf ./* # Remove default nginx files
COPY --from=build-stage /app/dist . # Copy built application
EXPOSE 80 # Expose port 80
CMD ["nginx", "-g", "daemon off;"] # Start nginx
```

<a id="nginxconf"></a>

### 3.2. nginx.conf

```nginx
server {
    listen 80;
    root /usr/share/nginx/html;
    index index.html index.htm;

    # Make site accessible from http://localhost/
    location / {
        try_files $uri $uri/ /index.html;
    }

    # Cache static files
    location ~* \.(jpg|jpeg|gif|png|ico|cur|gz|svg|svgz|mp4|ogg|ogv|webm|htc)$ {
      expires 1M;
      access_log off;
      add_header Cache-Control "public";
    }

    # Cache CSS and JS files
    location ~* \.(css|js)$ {
        try_files $uri =404;
        expires 1y;
        access_log off;
        add_header Cache-Control "public";
    }

    # Handle requests for files and return a 404 if they do not exist
    location ~ ^.+\..+$ {
        try_files $uri =404;
    }

    # Not found handler with custom 404 page
    error_page 404 /404.html;
    location = /40x.html {
    }

    # Error handler with custom 50x page
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
    }
}
```

<a id="contributing"></a>

## 4. Contributing

To contribute to this project, please see the [contributing guidelines](../../CONTRIBUTING.md).

<a id="license"></a>

## 5. License

This project is open and does not have a specific license. You may use this project as you wish.
