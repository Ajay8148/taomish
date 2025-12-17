FROM node:18-alpine AS build

WORKDIR /app

# Install dependencies
COPY package*.json ./
RUN npm install

# Copy source and build
COPY . .
RUN npm run build


FROM nginx:alpine

# Copy React build output to Nginx
COPY --from=build /app/build /usr/share/nginx/html

# Remove default Nginx config (optional but clean)
RUN rm /etc/nginx/conf.d/default.conf

# Add custom Nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 3000

CMD ["nginx", "-g", "daemon off;"]

