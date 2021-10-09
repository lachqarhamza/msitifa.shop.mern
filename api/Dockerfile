FROM node:lts-alpine@sha256:71a9ab5b02d8ddbcb56dab75d6d58720a2bb7536b4c72688b6443a22f2718676
RUN apk add dumb-init
ENV NODE_ENV production
WORKDIR /usr/src/app
COPY --chown=node:node . /usr/src/app
RUN npm ci --only=production
CMD ["dumb-init", "node", "app.js"]
