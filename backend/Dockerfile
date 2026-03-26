# ── Stage 1: Builder ──────────────────────────────
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

# ── Stage 2: Runtime (tiny final image) ──────────
FROM node:20-alpine AS runtime
WORKDIR /app

# Copy only production deps from builder
COPY --from=builder /app/node_modules ./node_modules
COPY . .

# Security: don't run as root
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

EXPOSE 3000
CMD ["node", "index.js"]
