FROM node:12 AS build

WORKDIR /app

COPY ./client/package.json ./

RUN npm install
COPY ./client ./
RUN npm run build

FROM nginx:1.19-alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]