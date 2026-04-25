# Stage 1 — Build the React app
FROM node:18-alpine AS builder

ENV CI=true
ENV WDS_SOCKET_PORT=0
ENV NODE_OPTIONS=--openssl-legacy-provider

WORKDIR /usr/app/client

COPY ./package.json ./
RUN npm install

COPY ./ ./

RUN npm run build

# Stage 2 — Serve with Nginx
FROM nginx:alpine

COPY --from=builder /usr/app/client/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]