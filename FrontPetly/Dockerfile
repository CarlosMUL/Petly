# Dockerfile para el frontend React + Vite
# Copiar en la raíz de FrontPetly como "Dockerfile"

FROM node:20-alpine AS builder
WORKDIR /app

# Copia dependencias primero (mejor cache)
COPY package*.json ./
RUN npm ci

# Copia el código y compila
COPY . .
RUN npm run build

# Imagen final con nginx
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
