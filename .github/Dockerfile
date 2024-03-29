FROM node:20 AS stage1
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY tests tests
COPY index.js index.js
RUN node_modules/.bin/mocha ./tests --recursive
RUN npm prune --production
FROM node:20-alpine
WORKDIR /app
COPY --from=stage1 --chown=node /app/node_modules node_modules
COPY --chown=node index.js index.js
EXPOSE 8080
USER node
CMD ["node", "index.js"]
