# Stage 1: Build
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Production server
FROM nginx:alpine
# Copy our custom Nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf
# Copy built static files from builder stage
COPY --from=builder /app/dist /usr/share/nginx/html
# Run on port 8080 as requested
EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]
