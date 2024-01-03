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
ENV NODE_ENV=production
WORKDIR /app
COPY --from=build-stage /app/package*.json ./
COPY --from=build-stage /app/dist  ./dist 
COPY --from=build-stage /app/node_modules ./node_modules
EXPOSE 3000
CMD [ "node", "dist/main.js" ]
