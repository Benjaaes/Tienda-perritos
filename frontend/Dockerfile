# ETAPA 1: Construcción (Builder)
FROM node:18-alpine AS build
WORKDIR /app
# Corregimos la ruta para que busque dentro de la carpeta frontend
COPY frontend/package*.json ./
RUN npm install
COPY frontend/ ./
RUN npm run build

# ETAPA 2: Servidor de Producción (Seguro y No-Root)
FROM nginxinc/nginx-unprivileged:alpine
# Copiamos el resultado de la construcción
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]
