# ETAPA 1: Construcción (Builder)
FROM node:18-alpine AS build
WORKDIR /app
# Buscamos explícitamente el archivo dentro de la subcarpeta del backend
COPY backend/package*.json ./
RUN npm install
COPY backend/ ./
# Si tu backend necesita compilarse (ej. TypeScript), descomenta la línea de abajo:
# RUN npm run build

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
