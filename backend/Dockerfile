FROM node:21-alpine AS weatherapp_backend

WORKDIR /app/backend

COPY . .

RUN npm install

EXPOSE 8080

CMD ["npm", "start"]
