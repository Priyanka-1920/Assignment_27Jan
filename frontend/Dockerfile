# frontend/Dockerfile

############################
# Stage 1: Build React App
############################
FROM node:18-alpine AS builder

LABEL org.opencontainers.image.description="ShopNow Frontend Build Stage"

WORKDIR /app

# Install dependencies
COPY package*.json ./

RUN npm ci --no-audit --prefer-offline

# Copy application source
COPY . .

# React environment variables
ENV PUBLIC_URL=
ENV REACT_APP_API_BASE_URL=/api

# Build React application
RUN npm run build


############################
# Stage 2: NGINX Runtime
############################
FROM nginx:1.24-alpine

LABEL org.opencontainers.image.description="ShopNow Frontend Runtime"

# Copy nginx configuration
COPY nginx/default.conf /etc/nginx/conf.d/default.conf

# Copy React build files
COPY --from=builder /app/build /usr/share/nginx/html

# Expose nginx port
EXPOSE 80

# Health check
HEALTHCHECK --interval=15s --timeout=5s --start-period=5s --retries=3 \
  CMD wget -qO- http://127.0.0.1/health || exit 1

# Start nginx
CMD ["nginx", "-g", "daemon off;"]