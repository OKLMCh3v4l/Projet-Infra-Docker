FROM node:lts-alpine as base
WORKDIR /app
COPY ./ ./

FROM base as dev
WORKDIR /app
ENV NODE_ENV=development
RUN npm install
EXPOSE 3002
CMD ["npm", "run", "dev"]

FROM base as build
WORKDIR /app
ENV NODE_ENV=production
RUN npm install && npm cache clean --force
RUN npm run build

FROM scratch as prod
WORKDIR /app
COPY --from=node:lts-alpine /usr/local/bin/node /usr/local/bin/node
COPY --from=build /app/node_modules ./node_modules
COPY --from=build /app/dist ./dist
USER 1000
EXPOSE 3002
CMD ["/usr/local/bin/node", "dist/main.js"]