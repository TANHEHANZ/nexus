# Dockerfile y Docker Compose Genérico

---

Este documento provee ejemplos genéricos de **Dockerfile** para frontend y backend, y un **docker-compose.yml** para levantar ambos servicios.

---

## 1. Dockerfile Backend Genérico

```dockerfile
# Etapa de desarrollo
FROM node:22-alpine AS development
WORKDIR /app

COPY package*.json ./
RUN npm install -g pnpm
RUN pnpm install

COPY . .
RUN npx prisma generate
RUN pnpm run build

# Etapa de producción
FROM node:22-alpine AS production
WORKDIR /app

COPY package*.json ./
RUN npm install -g pnpm
RUN pnpm install --only=production

COPY --from=development /app/dist ./dist
COPY prisma ./prisma
COPY .env.docker .env
RUN npx prisma generate

ENV TZ=America/La_Paz
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

CMD ["node", "dist/app.js"]
```

---

## 2. Dockerfile Frontend Genérico

```dockerfile
# Etapa de build
FROM node:20-alpine AS build
WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

# Etapa de producción
FROM nginx:alpine
COPY --from=build /app/dist/frontend/browser /usr/share/nginx/html
COPY nginx/nginx.conf /etc/nginx/conf.d/default.conf

ENV TZ=America/La_Paz
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

---

## 3. Docker Compose Genérico

```yaml
name: appdev
services:
  frontend:
    container_name: appdev-frontend
    image: 127.0.0.1:8082/appdev/frontend:latest
    restart: always
    ports:
      - "3016:80"
    command: ["nginx", "-g", "daemon off;"]
    networks:
      - appdev-net

  backend:
    container_name: appdev-backend
    image: 127.0.0.1:8082/appdev/backend:latest
    ports:
      - "3015:3210"
    restart: always
    command: >
      sh -c "npx prisma generate && npx prisma db push && node dist/app.js"
    networks:
      - appdevapi-net

networks:
  appdevapi-net:
    driver: bridge
    ipam:
      driver: default
      config:
        - subnet: 173.30.15.0/24

  appdev-net:
    driver: bridge
    ipam:
      driver: default
      config:
        - subnet: 173.30.16.0/24
```
