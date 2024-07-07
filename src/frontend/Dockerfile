# syntax=docker/dockerfile:1

# Build Vite app
# ------------------------------------
FROM node:20-alpine as build
WORKDIR /app
#COPY ./package*.json ./
#COPY ./vite.config.js ./
#COPY ./src ./src
COPY . .
#RUN npm ci
RUN npm install
RUN npm run build

# Run Vite app
# ------------------------------------
# FROM nginx:alpine
# COPY --from=build /app/dist /usr/share/nginx/html
# EXPOSE 8000
# CMD ["nginx", "-g", "daemon off;"]
FROM busybox:stable-musl
RUN adduser -D static
USER static
WORKDIR /home/static
COPY --from=build /app/dist .
CMD ["busybox", "httpd", "-f", "-v", "-p", "8080"]