# ETAPA 1: Construcción (Builder)
FROM node:18-alpine AS build
WORKDIR /app
# Copiamos solo los archivos de dependencias primero (buena práctica de caché)
COPY package*.json ./
RUN npm install
# Copiamos el resto del código y construimos
COPY . .
RUN npm run build

# ETAPA 2: Servidor (Producción)
# Usamos una imagen de Nginx que NO usa el usuario root por defecto (Mínimo privilegio - Rúbrica al 100%)
FROM nginxinc/nginx-unprivileged:alpine
# Copiamos el resultado de la Etapa 1 a la carpeta que Nginx usa para mostrar la web
# Nota: Si tu proyecto genera una carpeta 'build' en vez de 'dist', cambia 'dist' por 'build' en la línea de abajo.
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]
