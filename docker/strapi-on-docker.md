
### Strapi on Docker

#### Create a new Strapi project
`npx create-strapi-app@latest my-strapi-project --quickstart`

Create a .dockerignore file and add the following:
```dockerignore
.tmp/
.cache/
.git/
build/
node_modules/
data/
```

#### Create a Dockerfile
```dockerfile   

FROM node:16   #  or  FROM node:18.9.0-buster-slim
RUN apt-get update && apt-get install -y libvips-dev
ARG NODE_ENV=development
ENV NODE_ENV=${NODE_ENV}

WORKDIR /opt/
COPY ./package.json ./package-lock.json ./
ENV PATH /opt/node_modules/.bin:$PATH
RUN npm config set fetch-retry-maxtimeout 600000 -g && npm install

WORKDIR /opt/app
COPY ./ .
RUN ["npm", "run", "build"]
EXPOSE 1337
CMD ["npm", "run", "develop"]
```

Run docker build: `docker build -t mydockerstrapi:latest .`

Run container: `docker run -d -p 1337:1337 mydockerstrapi`



#### Resources
https://www.youtube.com/watch?v=HsojvBVk6JQ&t=2s
https://blog.dehlin.dev/docker-with-strapi-v4