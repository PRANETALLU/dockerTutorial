# Step 1: Use a compatible Node.js version for building
FROM node:18 as build-stage

# Step 2: Set the working directory
WORKDIR /app

# Step 3: Copy package files to install dependencies
COPY package.json package-lock.json ./

# Step 4: Install dependencies
RUN npm install

# Step 5: Copy the rest of the application code
COPY . .

# Step 6: Build the Vite app
RUN npm run build

# Step 7: Use an Nginx image to serve the built app
FROM nginx:alpine as production-stage

# Step 8: Copy the build output to Nginx's default HTML directory
COPY --from=build-stage /app/dist /usr/share/nginx/html

# Step 9: Expose port 80
EXPOSE 80

# Step 10: Start Nginx
CMD ["nginx", "-g", "daemon off;"]
