FROM node:10-slim@sha256:88932859e3d022d79161b99628c4c2c50e836437455e2d1b1a008d98367b10d6

# add curl for healthcheck
# add wait-for-it to delay start
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    curl \
    wait-for-it \
    && rm -rf /var/lib/apt/lists/*

# Add Tini for proper init of signals
ENV TINI_VERSION v0.19.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini

WORKDIR /app

# have nodemon available for local dev use (file watching)
RUN npm install -g nodemon

COPY package*.json ./

RUN npm ci \
 && npm cache clean --force \
 && mv /app/node_modules /node_modules

COPY . .

ENV PORT 80

ENV PGHOST localhost

EXPOSE 80

CMD ["/tini", "--", "node", "server.js"]
