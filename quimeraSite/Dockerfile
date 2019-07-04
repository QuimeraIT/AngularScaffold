FROM node:10.16.0-alpine as builder

WORKDIR /app
COPY ./package.json ./

ENV NODE_ENV=production

RUN npm ci
COPY . .

RUN npm run build:prod

FROM nginx:alpine
RUN rm -rf /usr/share/nginx/html/*
COPY nginx.conf /etc/nginx/nginx.conf
COPY --from=builder /app/dist/* /usr/share/nginx/html/


EXPOSE 8080/tcp

CMD ["nginx", "-g", "daemon off;"]