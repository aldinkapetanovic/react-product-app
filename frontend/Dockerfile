# Build stage
FROM node:latest AS build

WORKDIR /app

# Copy package.json and package-lock.json to the container
COPY package.json ./

COPY yarn.lock ./

# Install dependencies
RUN yarn

# Copy the rest of the application code
COPY . .

# Build the React app
RUN yarn build

# Serve stage
FROM nginx:latest

# Copy the custom nginx.conf file to the container
COPY .docker/nginx.conf /etc/nginx/nginx.conf

# Copy the built React app from the build stage to the nginx container
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]