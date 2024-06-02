FROM node:21-alpine

WORKDIR /app

COPY src src
COPY package.json package.json
COPY .eslintrc .eslintrc
COPY webpack.config.js webpack.config.js

RUN npm install

CMD ["npm", "start"]
