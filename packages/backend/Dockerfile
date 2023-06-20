# This dockerfile builds an image for the backend package.
# It should be executed with the root of the repo as docker context.
#
# Before building this image, be sure to have run the following commands in the repo root:
#
# yarn install
# yarn tsc
# yarn build:backend
#
# Once the commands have been run, you can build the image

FROM node:18-bullseye-slim

RUN --mount=type=cache,target=/var/cache/apt,sharing=locked \
    --mount=type=cache,target=/var/lib/apt,sharing=locked \
    apt-get update && \
    apt-get install -y --no-install-recommends libsqlite3-dev python3 build-essential && \
    yarn config set python /usr/bin/python3

RUN apt-get update && apt-get install -y python3-pip && pip3 install mkdocs-techdocs-core

USER node
WORKDIR /app

ENV NODE_ENV production

COPY --chown=node:node yarn.lock package.json packages/backend/dist/skeleton.tar.gz ./

COPY --chown=node:node ../../examples/ ./

RUN tar xzf skeleton.tar.gz && rm skeleton.tar.gz

RUN yarn cache clean

RUN --mount=type=cache,target=/home/node/.cache/yarn,sharing=locked,uid=1000,gid=1000 \
    yarn install --frozen-lockfile --production --network-timeout 300000

COPY --chown=node:node packages/backend/dist/bundle.tar.gz app-config*.yaml ./

RUN tar xzf bundle.tar.gz && rm bundle.tar.gz

CMD ["node", "packages/backend", "--config", "app-config.yaml", "--config", "app-config.production.yaml"]
