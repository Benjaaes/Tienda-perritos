# Servidor web ligero y seguro
FROM nginxinc/nginx-unprivileged:alpine

# Copiamos directamente tus archivos (index.html, app.js, etc.) a la carpeta pública de Nginx
COPY . /usr/share/nginx/html

# Exponemos el puerto
EXPOSE 8080

# Encendemos el servidor
CMD ["nginx", "-g", "daemon off;"]
