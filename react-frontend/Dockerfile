FROM node:16-alpine AS build
WORKDIR /app

COPY package.json package-lock.json ./
RUN npm ci && npm cache clean --force

COPY public ./public
COPY src ./src
RUN npm run build

FROM nginx:alpine
RUN addgroup -S appuser && adduser -S appuser -G appuser \
 && mkdir -p /var/cache/nginx/client_temp /var/cache/nginx/proxy_temp \
 && chown -R appuser:appuser /var/cache/nginx
WORKDIR /usr/share/nginx/html

COPY --from=build /app/build ./
VOLUME ["/etc/nginx/conf.d"]
USER appuser


