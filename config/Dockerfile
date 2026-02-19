# use the official Bun image
# see all versions at https://hub.docker.com/r/oven/bun/tags
FROM oven/bun:1.2.8-alpine AS base
WORKDIR /usr/src/app
# install dependencies into temp directory
# this will cache them and speed up future builds
FROM base AS build
RUN mkdir -p /app

COPY package* *.lock *.sh ./app/
COPY . /app/
RUN cd /app && bun --bun install --frozen-lockfile && bun --bun run build


FROM oven/bun:1.2.8-alpine
WORKDIR /usr/src/app
COPY --from=build /app/build ./
COPY --from=build /app/entry.sh ./entry.sh
COPY --from=build /app/node_modules ./node_modules

ENTRYPOINT [ "./entry.sh" ]

# CMD [ "ls" ]

EXPOSE 4353
