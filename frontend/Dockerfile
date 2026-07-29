# Stage 1: Build the React/Vite app
FROM node:20-alpine AS build

WORKDIR /application

COPY package*.json ./

RUN npm ci

COPY . .

RUN npm run build

# Stage 2: Serve using Nginx
FROM nginx:stable-alpine

# Copy the Vite build output
COPY --from=build /application/dist /usr/share/nginx/html

# Copy nginx configuration
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]