
FROM node:16-alpine

WORKDIR /usr/src/app

COPY ./package*.json ./

RUN npm install

COPY . .

EXPOSE 8080

CMD [ "index.js" ]


#FROM node:16-slim
# FROM node:16-alpine

# WORKDIR /usr/src/app

# COPY ./package*.json ./

# RUN npm install

# COPY . .

# EXPOSE 8080

# CMD [ "index.js" ]


