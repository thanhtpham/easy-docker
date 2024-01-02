# Dockerize Next.js App
This is a simple boilerplate to dockerize a Next.js app.

## Table of Contents

1. [Installation](#installation)
2. [Usage](#usage)
3. [Explanation](#explanation)
4. [Contributing](#contributing)
5. [License](#license)

<a id="installation"></a>

## 1. Installation

Clone the repository. You can run `npm install` to install the dependencies and `npn run dev` to start the development server.

Requirements:

- Docker
- Node.js (v20)

> **Note**: I use [ts-nextjs-tailwind-starter](https://github.com/theodorusclarence/ts-nextjs-tailwind-starter) as the starter template. You can use any template you want.

<a id="usage"></a>

## 2. Usage

```bash
# Build the image
docker build -t <image-name> .

# Run the container
docker run -d -p <host-port>:3000 <image-name>
```

> **Note**: you can use `Dockerfile` and `.dockerignore` in the root directory for your project.

<a id="explanation"></a>

## 3. Explanation

### 3.1. Simple Dockerfile

```dockerfile
FROM node:20-alpine
LABEL author="Thanh Pham <thanhtpham99@gmail.com>"

WORKDIR /app

COPY package*.json ./
RUN npm ci \
    && npm cache clean --force

COPY . .
RUN npm run build

EXPOSE 3000

CMD ["yarn", "start"]
```

This is a simple Dockerfile. It is not recommended to use this in production, because it will install all the dependencies in the container. This will increase the size of the image and the build time. 

### 3.2. Multi-stage Dockerfile

```dockerfile
# Base image
FROM node:20-alpine as base
LABEL author="Thanh Pham <thanhtpham99@gmail.com>"
WORKDIR /app
COPY package*.json ./
RUN npm ci && npm cache clean --force

# Build stage
FROM base as build-stage
LABEL author="Thanh Pham <thanhtpham99@gmail.com>"
COPY . .
RUN npm run build \
  && rm -rf node_modules \
  && npm ci --only=production

# Production stage
FROM node:20-alpine as production-stage
LABEL author="Thanh Pham <thanhtpham99@gmail.com>"
WORKDIR /app
COPY --from=build-stage /app/package*.json ./
COPY --from=build-stage --chown=nextjs:nodejs /app/.next ./.next
COPY --from=build-stage /app/public ./public
COPY --from=build-stage /app/node_modules ./node_modules
ENV NODE_ENV=production
EXPOSE 3000
CMD ["npm", "start"]
```

- **Base image**: This is the base image for the Docker image. It will install the dependencies and cache it. This will reduce the build time for the next stage.
- **Build stage**: This is the build stage. It will copy the source code and build the application. It will also remove the `node_modules` and install the production dependencies only to reduce the size of the image.
- **Production stage**: This is the production stage. It will copy the built application from the build stage and run the application.

This is a multi-stage Dockerfile. It is recommended to use this in production, because it will install the dependencies in the build stage and copy the built application to the production stage. This will reduce the size of the image and the build time. (Down from 1.74Gb to 0.74Gb)

<a id="contributing"></a>

## 4. Contributing

To contribute to this project, please see the [contributing guidelines](../../.github/CONTRIBUTING.md).

<a id="license"></a>

## 5. License

This project is open and does not have a specific license. You may use this project as you wish.

