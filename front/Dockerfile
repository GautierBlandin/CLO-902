# Step 1: Build the Angular app
FROM node:11 AS build

WORKDIR /app

# Copy package.json and package-lock.json (or yarn.lock) for installing dependencies
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the Angular app for production
RUN npm run build:prod
RUN ls -la dist/front


# Step 2: Set up the nginx server to serve the built app
FROM nginx:1.21-alpine

# Copy the built Angular app to the nginx html folder
COPY --from=build /app/dist/front /usr/share/nginx/html
RUN ls -la /usr/share/nginx/html

# Copy the nginx configuration file
COPY ./nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80 for the nginx server
EXPOSE 80

# Start the nginx server
CMD ["nginx", "-g", "daemon off;"]
