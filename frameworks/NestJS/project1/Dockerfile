FROM node:14-alpine As prod

ENV PORT_API=3000

EXPOSE ${PORT_API}

RUN apk add --no-cache tini
# RUN apk add --update curl && <other required packages>

WORKDIR /node
# RUN mkdir node && chown -R node:node .

COPY package.json package-lock*.json ./
RUN chown -R node:node . \
    && npm install -g @nestjs/cli
USER node
RUN npm install --only=production \
    && npm cache clean --force

WORKDIR /node/app
COPY --chown=node:node . .

ENTRYPOINT [ "/sbin/tini", "--" ]
CMD ["node", "dist/main"]

# can run with: docker run --name nest1 -e PORT_API=3002 -p 3002:3002 --rm nest1
#   - the app is setup to listen on PORT_API or default 3000

FROM prod as dev
WORKDIR /node
RUN npm install --only=development
WORKDIR /node/app
CMD ["npm", "run", "start:dev"]

