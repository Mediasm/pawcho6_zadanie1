# Stage 1: Build the application
FROM node:alpine AS builder
WORKDIR /home/node/app
COPY package.json ./
RUN npm install --only=production
COPY app.js ./
RUN cp /usr/local/bin/node /home/node/app/node
RUN chmod +x /home/node/app/node

# Stage 2: Run the application
FROM node:alpine 
LABEL maintainer="Artem Smolii"
ARG VERSION
ENV VERSION=${VERSION:-v1.0.0}
WORKDIR /home/node/app
COPY --from=builder /home/node/app .
USER node
EXPOSE 5000
HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 \
    CMD curl -f http://localhost:5000/ || exit 1
CMD ["/home/node/app/node", "app.js"]