# Build site with node image
FROM node:lts-alpine as node-builder
WORKDIR /usr/src/app
COPY curriculum-front/package*.json ./
RUN ls -l
RUN npm install
COPY curriculum-front ./
RUN ls -l
RUN npm run build

# Use nginx image to serve the static files
# (and proxy to the back-end too!)
FROM nginx:1.18
WORKDIR /usr/share/nginx/html
COPY --from=node-builder /usr/src/app/dist .
EXPOSE 80