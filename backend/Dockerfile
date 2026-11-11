# Production Dockerfile for CampusOS Express Backend
FROM node:20-alpine

WORKDIR /app

# Install curl for healthcheck support
RUN apk add --no-cache curl

# Copy dependency manifests first (layer cache optimisation)
COPY package*.json ./

# Install production dependencies only
RUN npm ci --omit=dev

# Copy application source
COPY . .

# Create a non-root user for security
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

# Expose backend port
EXPOSE 5000

ENV NODE_ENV=production
ENV PORT=5000

CMD ["node", "src/server.js"]
