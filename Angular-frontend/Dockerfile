# Use the official Node.js 18 image as the base image
FROM node:18

# Install NGINX
RUN apt-get update && apt-get install -y nginx && rm -rf /var/lib/apt/lists/*

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json (if available)
COPY package*.json ./

# Update npm to the required version
RUN npm install -g npm@10.8.1

# Install project dependencies
RUN npm install

# Copy the rest of the application code to the working directory
COPY . .

# Build the Angular application with optimizations
RUN npm run build 

# Remove the default NGINX configuration file
RUN rm /etc/nginx/sites-available/default

# Copy the custom NGINX configuration file to the container
COPY nginx.conf /etc/nginx/sites-available/default

# Copy the built Angular application to the NGINX html directory
RUN cp -r /usr/src/app/dist/angular-frontend/* /var/www/html/

# Expose port 80 to the outside world
EXPOSE 80

# Command to start NGINX
CMD ["nginx", "-g", "daemon off;"]




