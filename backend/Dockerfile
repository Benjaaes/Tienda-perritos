# ETAPA 1: Construcción (Builder)
FROM node:18-alpine AS build
WORKDIR /app
# Buscamos en la carpeta actual donde nos paró el robot
COPY package*.json ./
RUN npm install
COPY . .

# ETAPA 2: Ejecución Ligera
FROM node:18-alpine
WORKDIR /app

# CREAR USUARIO NO ROOT (Mínimo privilegio - Exigencia del profesor)
RUN adduser -D miusuarioapp
USER miusuarioapp

# Copiamos las dependencias y el código desde la etapa de construcción
COPY --from=build /app/node_modules ./node_modules
COPY --from=build /app ./

EXPOSE 3001
CMD ["node", "server.js"]
