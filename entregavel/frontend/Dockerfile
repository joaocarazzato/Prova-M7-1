FROM node:latest

WORKDIR /frontend

COPY . .

RUN npm i

COPY . .

CMD ["node", "server.js"]