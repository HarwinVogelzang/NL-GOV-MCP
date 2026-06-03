FROM node:22-alpine

WORKDIR /app

COPY package*.json ./

RUN npm ci --ignore-scripts

COPY . .

RUN npm run build

RUN addgroup -g 1001 -S nodejs && adduser -S nodejs -u 1001
USER nodejs

ENV NODE_ENV=production
ENV MCP_TRANSPORT=streamable-http
ENV NL_GOV_HTTP_PORT=3333
ENV NL_GOV_TIMEZONE=Europe/Amsterdam

EXPOSE 3333

HEALTHCHECK --interval=30s --timeout=5s --start-period=10s --retries=3 \
  CMD wget --no-verbose --tries=1 --spider http://localhost:3333/health || exit 1

CMD ["npm", "run", "dev:streamable-http"]