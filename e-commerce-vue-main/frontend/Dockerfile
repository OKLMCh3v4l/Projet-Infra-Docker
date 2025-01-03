FROM node:lts-alpine as base
WORKDIR /app
COPY ./package.json ./
RUN npm install

FROM base as dev
COPY ./ ./
EXPOSE 8080
CMD ["npm", "run", "dev", "--", "--host"]

FROM base as build
ENV NODE_ENV=production
COPY ./ ./
RUN npm run build

FROM nginx:stable-alpine as prod
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]