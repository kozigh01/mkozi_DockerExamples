FROM node:12-alpine As base

LABEL org.opencontainers.image.created='2020-07-11'       
LABEL org.opencontainers.image.authors='mkozi.gh01@gmail.com'
LABEL org.opencontainers.image.url='https://github.com/kozigh01/mkozi_DockerExamples'
LABEL org.opencontainers.image.documentation='https://github.com/kozigh01/mkozi_DockerExamples/blob/master/readme.md'
LABEL org.opencontainers.image.version='0.0.1'
LABEL org.opencontainers.image.vendor='mkozi'
LABEL org.opencontainers.image.title='Docker Exeample - NestJS'
LABEL org.opencontainers.image.description='Reference add for NestJS in Docker'

ENV NODE_ENV=production
ENV PORT_API=3000
EXPOSE ${PORT_API}

RUN apk add --no-cache tini 
# RUN apk add --update curl && <other required packages>
# RUN apt-get update -qq && apt-get install -qy curl --no-install-recommends

WORKDIR /node

COPY package*.json ./
RUN chown -R node:node .
RUN npm config list \
    && npm ci \
    && npm cache clean --force

ENV PATH=/node/node_modules/.bin:$PATH

ENTRYPOINT [ "/sbin/tini", "--" ]


#----------------
#   Development
#----------------
# we don't COPY in this stage because for dev you'll bind-mount anyway
# this saves time when building locally for dev via docker-compose
#   * can run with: docker run --name nest1 -e PORT_API=3002 -p 3002:3002 --rm nest1
#       - the app is setup to listen on PORT_API or default 3000
FROM base as dev
ENV NODE_ENV=development
RUN npm install --only-development
WORKDIR /node/app
CMD ["npm", "run", "start:debug"]


#-----------------------------------
#   Test
#
#   run with: 
#       docker build --target test -t nestjs:test .
#       docker run nestjs:test
#-----------------------------------
FROM dev as test
COPY --chown=node:node  . .
USER node
CMD ["npm", "run", "test"]


#-----------------------------------
#   Source - used by prod
#-----------------------------------
FROM dev as source
COPY --chown=node:node  . .
RUN npm run build
RUN ls -lah dist


#----------------
#   Production
#----------------
FROM base as prod
WORKDIR /node
COPY --chown=node:node --from=source /node/app/dist/ /node/dist/
RUN pwd && ls -lah && ls -lah dist
USER node
CMD ["node", "/node/dist/main.js"]
# CMD tail -f /dev/null