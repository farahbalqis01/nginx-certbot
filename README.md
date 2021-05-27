# Introduction

To be modified for use with Farah's website

This is a modified fork for [nginx-certbot](https://github.com/wmnnd/nginx-certbot) that can be used as a template for deploying static websites quickly on a server using Docker with nginx and Let's Encrypt. The Docker compose file will also check and auto-renew certificates if they need to be reprovisioned.

The web root is found in `./data/web`. This project allows the deployment of an https site secured with Let's Encrypt using Docker.

A guide to how everything fits together can be found [here](https://medium.com/@pentacent/nginx-and-lets-encrypt-with-docker-in-less-than-5-minutes-b4b8a60d3a71).

# Dependencies

## Docker

* [Follow the installation guide to install Docker.](https://docs.docker.com/engine/install/)

* Follow [post installation steps](https://docs.docker.com/engine/install/linux-postinstall/) in the official Docker guide so the user does not need to invoke sudo. Permission issues may follow if executing the scripts with sudo privileges.

## Docker Compose

This is a replacement of the `docker-compose` package that may be installed with Docker. Docker compose should be updated explicitly using the [official guide](https://docs.docker.com/compose/install/#alternative-install-options) as the default installed version is not up to date, resulting in compatibility issues.

# Initial steps to reuse repository.

1. All configuration files can be obtained from the `nginx-certbot` submodule folder. Find all instances of the `example.org` and replace with new domain in `init-letsencrypt.sh`, `docker-compose.yml`, and `.data/nginx/app.conf`.
2. Set email address in `init-letsencrypt.sh` with contact of person responsible for the website.
3. In this project, the web folder is placed in `./data/web`. Replace all contents in this folder with the site files.

# Execution to build site

None of these commands require sudo privileges. Make sure dependencies are installed and initial steps have been completed.

1. Run `./init-letsencrypt.sh`. If errors occur here in certificate retrieval, open the script and change staging to 0 before continuing to debug. Let's Encrypt will allow up to 20 certificate retrievals before imposing a 7-day suspension on the domain's certificate generation process.

2. Run `docker-compose up` to check if site is properly deployed. Add `-d` to the options to run in detached mode after confirming site works.

# Quick commands

## Stop all containers

`docker-compose stop`

## Start container and rebuild if changes made

`docker-compose up --build -d`
