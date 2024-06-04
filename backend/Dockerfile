FROM node:21-alpine

WORKDIR /app

COPY src src
COPY package.json package.json

RUN npm install

ENV APPID="01de6726130b583aa51b03d44414d800"

EXPOSE 9000

CMD ["npm", "start"]
