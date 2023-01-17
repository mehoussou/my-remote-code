
FROM node:16-alpine

WORKDIR /usr/src/app

COPY ./package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD [ "npm", "start" ]



#FROM node:16-slim
# FROM node:16-alpine

# WORKDIR /usr/src/app

# COPY ./package*.json ./

# RUN npm install

# COPY . .

# EXPOSE 3000

# CMD ["npm","start"]



