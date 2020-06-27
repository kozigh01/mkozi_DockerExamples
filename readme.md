# Docker / Docker-Compose

## Notes
* docker-compose.yml file uses environment variables
  * Docker doc: [Environemnt variables in Comopse](https://docs.docker.com/compose/environment-variables/)
  * can also over-ride: $ ENV_VAR=var-value docker-compose up

## Redis
Instructions:
* $ docker-compose up -d
* $ docker-compose exec redis bash
* # redis-cli
* Now run redis commands: [redis](https://redis.io/commands) | 

## Elasticsearch
Source: [udemy](https://www.udemy.com/course/elasticsearch-7-and-elastic-stack/)

## Frameworks 

### NestJS
* Dockerfile example: [blog](https://medium.com/@basakabhijoy/dockerise-a-nestjs-app-2b7f42fc333f) | [blog](https://blog.logrocket.com/containerized-development-nestjs-docker/)
* Docker env info: [Docker ARG, ENV and .env - a Complete Guide](https://vsupalov.com/docker-arg-env-variable-guide/)
* NestJS env info: [NestJS docs](https://docs.nestjs.com/techniques/configuration)


## Other Projects
* GraphQL w/ Postgres, api, web: [github](https://github.com/kozigh01/udemy_GraphQForBeginnersWithJavascript)
* Bret Fisher - creating/using linux user in dockerfile: [github](https://github.com/BretFisher/dockercon19/blob/master/2.Dockerfile)
* Environment configs, variables and entrypoints: [udemy](https://www.udemy.com/course/docker-mastery/learn/lecture/13909150) | [blog](https://www.oreilly.com/content/3-docker-compose-features-for-improving-team-development-workflow/)