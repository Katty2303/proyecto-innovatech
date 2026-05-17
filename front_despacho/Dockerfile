# ========================================================
# ETAPA 1: Construcción y compilación (Builder)
# ========================================================
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# ========================================================
# ETAPA 2: Servidor web de producción seguro (Nginx)
# ========================================================
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html

# BUENA PRÁCTICA DE SEGURIDAD (Mínimo Privilegio): 
# Modificamos los archivos internos de Nginx para que corra SIN ser usuario administrador root
RUN touch /var/run/nginx.pid && \
    chown -R nginx:nginx /var/run/nginx.pid /var/cache/nginx /var/log/nginx

# Cambiamos oficialmente al usuario limitado de Nginx
USER nginx

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]