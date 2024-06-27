# Build stage
FROM registry.access.redhat.com/ubi8/nodejs-18:1-110.1719303984 AS build

WORKDIR /app

# Copy package.json and package-lock.json to the container
COPY package*.json ./

RUN chmod -R ugo+rw /app/

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the React app
RUN npm run build

# Serve stage
FROM registry.access.redhat.com/ubi8/nginx-124:1-12.1717586547


# Copy the built React app from the build stage to the nginx container
COPY --from=build /app/build /opt/app-root/src

# Expose port 80
EXPOSE 8080

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
