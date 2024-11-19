## Overview

This repo contains common docker-compose files useful for my local development tool-chain.

## Images
* Seq - Logging Container
* Postgres - Database
* Wiremock.net - Server for mocking and stubbing
* Keycloak - Auth and permissions server

Note - can also use normal wiremock: `docker run -it --rm  -p 8443:8443 --name wiremock wiremock/wiremock:3.9.1 --https-port 8443 --verbose`

## To Run

`docker compose -f docker-compose.wiremock.yml -f docker-compose.seq.yml -f docker-compose.postgres.yml -f docker-compose.keycloak.yml up`
