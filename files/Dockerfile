FROM node:latest

# Create app dir
WORKDIR /usr/src/app

# Install app dependencies
COPY package*.json ./

RUN npm install

# Bundle app source
COPY . .

EXPOSE 8084
CMD [ "npm", "start" ]
