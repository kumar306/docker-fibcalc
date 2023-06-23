FROM node:16-alpine as builder
RUN mkdir -p /home/node/app
WORKDIR /home/node/app
COPY --chown=node:node ./package.json ./
RUN npm install
COPY --chown=node:node ./ ./
RUN npm run build

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /home/node/app/build usr/share/nginx/html

# for prod, we are having another nginx instance at port 3000 at react server for serving static assets
# built the code and copying it into nginx default directory where assets are served