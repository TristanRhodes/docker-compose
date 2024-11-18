## Overview

This repo contains common docker-compose files useful for my local development tool-chain.

## Images
* Seq - Logging Container
* Postgres - Database
* Wiremock - Server for mocking and stubbing

## To Run

`docker compose -f docker-compose.wiremock.yml -f docker-compose.seq.yml -f docker-compose.postgres.yml up`

## Pending
* An auth server. Something providing OAuth identities and key management.