# stage 1: build react app first
FROM node:lts-alpine@sha256:71a9ab5b02d8ddbcb56dab75d6d58720a2bb7536b4c72688b6443a22f2718676 AS build
WORKDIR /usr/src/app
ENV PATH /usr/src/app/node_modules/.bin:$PATH
COPY package.json ./
RUN npm install --silent --production
COPY . ./
RUN npm run build

# stage 2: build the final image and copy the react build files
FROM nginx:1.17.8-alpine AS prod
COPY --from=build /usr/src/app/build /usr/share/nginx/html
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx/nginx.conf /etc/nginx/conf.d
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
