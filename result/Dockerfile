FROM node:21-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install --only=production

COPY . .

EXPOSE 80

CMD ["node", "server.js"]
