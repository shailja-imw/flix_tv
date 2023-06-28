
FROM node:lts-alpine

WORKDIR /app1

COPY package*.json ./

RUN npm install

COPY . ./

RUN npm run build

EXPOSE 3000

CMD [ "npm", "start" ]
