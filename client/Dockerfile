# Multi-Step Docker Build  

# Specifying baseImage - 
# Here `builder` is the build stage name.
FROM node:alpine as builder 

# Specifying working directory - 
WORKDIR /usr/app

# Copying only package.json to working directory.
# To install project dependencies, npm needs only this file.
COPY ./package.json ./

# Installing project dependencies - 
RUN npm install

# Copying rest of the files to current working directory - 
COPY ./ ./

# Building the project - 
RUN npm run build

# -------------------------------------------------------------------------------------------------------------- #

# 2nd build stage starts from here - 
FROM nginx 

# Overriding the `default.conf` file that comes with `nginx` image with our custom one.
# Note - By default, nginx listens on port 80. 
# We changed it to port 3000 in our custom `default.conf` file.
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

# Copying the output from previous build stage (--from=<build_stage_name>) - 
COPY --from=builder /usr/app/build /usr/share/nginx/html
