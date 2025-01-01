## Overview

This repo contains common docker-compose files useful for my local development tool-chain.

## Images
* Seq - Local log sink
* Postgres - Database
* Wiremock.net - Server for mocking and stubbing
* Keycloak - Auth and permissions server

## Keycloak Setup (Windows)
For local keycloak to work properly as an OIDC server with another application, it needs to be running HTTPS with a valid, trusted certificate, otherwise you will recieve an SSL error at runtime. To support this, you will need to generate a certificate for localhost and add it to trusted root, and load this certificate into Keycloak.

This section is based off these articles: 
* https://cloudspinx.com/run-keycloak-in-docker-or-podman-with-lets-encrypt-ssl/
* https://www.supportyourtech.com/articles/how-to-add-certificate-to-trusted-root-windows-10-a-step-by-step-guide/

Install `Bash` if you don't already have it as part of Git.

In `Bash` navigate to the root docker-compose directory for this repo.

> mkdir ssl && cd ssl

Generate private key.

> openssl genrsa -out local.keycloak.key

Generate CSR and private key files by running the following commands.

> openssl req -new -key local.keycloak.key -out local.keycloak.csr

Sign the certificate using a private key and CSR:

> openssl x509 -req -in local.keycloak.csr -signkey local.keycloak.key -days 36500 -out local.keycloak.crt.

Update your volumes int `docker-compose.keycloak.yml` to point at the local certificate:
>  - ./ssl/local.keycloak.crt:/opt/keycloak/conf/server.crt
>  - ./ssl/local.keycloak.key:/opt/keycloak/conf/server.key

Finally, import the SSL Certificate into your `Trusted Root Certification Authorities` via the `MMC.exe` => `Certificates` plugin. 

## To Run
`docker compose -f docker-compose.wiremock.yml -f docker-compose.seq.yml -f docker-compose.postgres.yml -f docker-compose.keycloak.yml up`

## Connections

### Seq
Url: https://localhost:5030

### Postgres (PgAdmin)
Adminer: https://localhost:8443
Username: user@local.com
Password: password

Postgres: https://localhost:5432
Username: pgadmin
Password: password

### Wiremock.net
Url: https://localhost:8080

### Keycloak
Url: https://localhost:8443
Username: admin
Password: password
