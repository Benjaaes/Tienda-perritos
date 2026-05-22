# ETAPA 1: Construcción (Builder)
FROM node:18 AS build
WORKDIR /app

# Buscamos en la carpeta actual donde nos paró el robot
COPY package*.json ./
RUN npm install --legacy-peer-deps

COPY . .
RUN npm run build

# ETAPA 2: Servidor de Producción (Seguro y No-Root)
FROM nginxinc/nginx-unprivileged:alpine
# Copiamos el resultado de la construcción
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]
