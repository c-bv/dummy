FROM node:20-alpine AS build

WORKDIR '/app'
COPY package.json .
COPY package-lock.json .

COPY . .

RUN npm install --loglevel verbose

RUN npm run build

# stage 2 - build the final image and copy the react build files
FROM nginx:1.17.8-alpine
COPY --from=build /app/dist /usr/share/nginx/html


RUN rm /etc/nginx/conf.d/default.conf
COPY .nginx/nginx.conf /etc/nginx/conf.d

# Start Nginx server
CMD ["nginx", "-g", "daemon off;"]