FROM node:20-alpine AS build

WORKDIR '/app'
COPY package.json .
COPY package-lock.json .

COPY . .

RUN npm install --loglevel verbose

RUN npm run build

# stage 2 - build the final image and copy the react build files
FROM nginx:1.17.8-alpine
COPY --from=build /app/build /usr/share/nginx/html

# Default port exposure
EXPOSE 80

RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d

# Start Nginx server
CMD ["nginx", "-g", "daemon off;"]