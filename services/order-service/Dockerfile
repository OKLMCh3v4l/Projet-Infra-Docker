FROM node:lts-alpine as base
WORKDIR /app
COPY ./ ./

FROM base as dev
WORKDIR /app
ENV NODE_ENV=development
RUN npm install
EXPOSE 3002
CMD ["npm", "run", "dev"]

FROM base as prod
ENV NODE_ENV=production
RUN npm install && npm cache clean --force
EXPOSE 3002
CMD ["npm", "start"]