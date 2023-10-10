FROM node:14-alpine 

# specify working directory to run commands
WORKDIR /usr/app

# copying package file first to install depen and cache to image. 
# helps avoid unnecesary rebuilds of depen when changes are made 
# only to index.js or other src files
COPY ./package.json ./
# install dependencies
RUN npm install

COPY ./ ./

# path to copy from(relative to build context) to(inside container)

CMD ["npm", "start"] 