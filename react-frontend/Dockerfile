FROM node:16-alpine AS build
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn install --frozen-lockfile && yarn cache clean
COPY public ./public
COPY src ./src
RUN yarn build

FROM nginx:alpine
RUN addgroup -S appuser && adduser -S appuser -G appuser
WORKDIR /usr/share/nginx/html
COPY --from=build /app/build ./
VOLUME ["/etc/nginx/conf.d"]
USER appuser

