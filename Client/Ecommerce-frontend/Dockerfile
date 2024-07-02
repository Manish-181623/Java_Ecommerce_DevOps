# Stage 1: Build the Angular application
FROM node:14 AS build

# Set the working directory
WORKDIR /app

# Copy the package.json and package-lock.json
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the Angular application
RUN npm run build --prod

# Stage 2: Serve the application with Nginx
FROM nginx:alpine

# Copy the built Angular application from the build stage
COPY --from=build /app/dist/ngspringshoppingstore /usr/share/nginx/html

# Copy the default Nginx configuration
COPY nginx.conf /etc/nginx/nginx.conf

# Expose port 80
EXPOSE 80

# Start Nginx server
CMD ["nginx", "-g", "daemon off;"]
