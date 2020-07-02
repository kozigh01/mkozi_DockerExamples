FROM node:14-alpine As development

ENV PORT_API=3000

EXPOSE ${PORT_API}

WORKDIR /app
# RUN mkdir app && chown -R node:node .

COPY package.json ./
RUN chown -R node:node
USER node
RUN npm install && npm cache clean --force

COPY --chown=node:node . .

CMD ["npm", "run", "start:dev"]

# can run with: docker run --name nest1 -e PORT_API=3002 -p 3002:3002 --rm nest1
#   - the app is setup to listen on PORT_API or default 3000

