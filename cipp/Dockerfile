FROM node:16-alpine3.15 as build-stage
RUN apk update
RUN apk add git
WORKDIR /app
RUN git clone -b dev https://github.com/redanthrax/CIPP.git .
COPY ./noauth.patch /app/noauth.patch
RUN git apply noauth.patch
RUN npm install
RUN npm run build

FROM nginx:latest
COPY --from=build-stage /app/build /usr/share/nginx/html
COPY ./default.conf /etc/nginx/conf.d/default.conf
