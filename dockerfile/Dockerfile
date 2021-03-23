FROM node:14

# Creation de l'applicaiton directory
WORKDIR /usr/src/app

# Installtion des deps
COPY package.json ./
COPY package-lock.json ./

RUN npm install

# Bundle app source
COPY . .

EXPOSE 8080

# Run serveur
CMD [ "node", "app.js" ]