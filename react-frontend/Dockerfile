# builder stage
FROM node:16-alpine AS builder
WORKDIR /app

# copy package.json + package-lock.json (not yarn.lock) and your .env
COPY package.json package-lock.json .env ./

# install dependencies
RUN npm ci && npm cache clean --force

# copy source and build
COPY public ./public
COPY src    ./src
RUN npm run build


# 2) serve with nginx
FROM nginx:alpine
COPY --from=builder /app/build /usr/share/nginx/html
EXPOSE 80

