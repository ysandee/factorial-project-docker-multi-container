#### Step 1

# Use an existing docker image as base
FROM node:alpine as builder

# Specify WORKDIR
WORKDIR '/factorial-project'

# Copy the package.json from your work directory to the container's work directory
# Until we copy the package.json file to container work directory, npm install will not work
COPY ./package.json .

# Install dependencies
RUN npm install

# Copy the source code from your work directory to the container's work directory
COPY ./ ./

# Startup Command
RUN npm run build

#### Step 2
# Copy the build directory to Nginx directory

# Fetch nginx image from docker hub
FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /factorial-project/build /usr/share/nginx/html
