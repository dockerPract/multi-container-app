FROM node:16-alpine as builder
USER root
RUN mkdir -p /usr/app && chown -R node:node /usr/app
USER node
RUN mkdir -p /usr/app
WORKDIR /usr/app
COPY --chown=node:node ./package.json ./
RUN npm install
COPY --chown=node:node ./ ./
RUN npm run build


FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html