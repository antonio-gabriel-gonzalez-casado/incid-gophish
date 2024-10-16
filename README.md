# GoPhish for Production

## Features
- [Docker](https://www.docker.com/)
- [Nginx](https://www.nginx.com/)
- [Let's Encrypt](https://letsencrypt.org/)
- [MySQL Database](https://www.mysql.com/)
- [Postfix](http://www.postfix.org/)
- [Adminer database management UI](https://www.adminer.org/)
- Tested to launch on an Ubuntu 18.04 LTS Server

## Requirements
* For local setup, Get the right flavor of Docker for your OS...
    - [Docker for Mac](https://docs.docker.com/docker-for-mac/install/)
    - [Docker for Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
    - [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)

    **Note:** The recommended requirement for deployment of this project is 4 GB RAM.
    For Docker for Mac, this can be set by following these steps:

    Open Docker > Preferences > Advanced tab, then set memory to 4.0 GiB

* A registered domain name

## Setup locally
- Create your env file
    - `cp etc/env.dist .env`
- Build containers
    -  `docker compose build`
- Run GoPhish
    - `docker compose up -d`
- Restart proxy to reflect changes
    - `docker exec -it gophish-proxy service nginx restart`
- GoPhish admin UI is running on `localhost` & `localhost:3333`
    - Important: Once Gophish is started, you must access the logs of the docker container that created it and look for the initial administrator password.
- Phishing server is running on `localhost:8080`
- Adminer UI is running on `localhost:9000`

### Stop and Remove project containers
- Stop all containers
    - `docker compose stop`
- Remove all containers
    `docker compose down`

