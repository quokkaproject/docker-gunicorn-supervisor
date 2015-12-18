# Quokka CMS
##Running with supervisor and gunicorn in a docker container

## Requirements

- git
- docker
- docker-compose


## Prepare

```bash
git clone --recursive https://github.com/quokkaproject/docker-gunicorn-supervisor.git
cd docker-gunicorn-supervisor
docker-compose build
```

## Configure (optional)

It is with the default configurations for running, but you can change configs editing **docker-compose.yml** file.

Normally you will expose this service using a server like **nginx**, by default it runs using 5000 port, you change the port mapping in docker-compose.yml

```yaml

    ports:
        # "HOST_PORT: CONTAINER_PORT"
        - "5000:5000"

```

Any quokka configurations can be replaced using environment

```yaml
    environment:
        - QUOKKA_MONGODB_HOST=mongo
        - QUOKKA_MONGODB_DB=quokka_db
        - QUOKKA_DEFAULT_THEME=pure
```

## Adding themes (optional)

Lets say you want to add a new theme, in example the **material** theme.

Add the theme submodule to themes folder

```bash
git submodule add https://github.com/quokkaproject/theme_material themes/material
git submodule init
```

Create the mapping adding "./themes/material:/quokka/quokka/themes/material" to volumes in docker-compose.yml

```yaml
    volumes:
        ...
        - ./themes/material:/quokka/quokka/themes/material
```

Change the DEFAULT_THEME config using env vars

```yaml
    environment:
        - QUOKKA_DEFAULT_THEME=material
```

> optionally you can use local_settings.py file to rewrite config variables

## Adding modules (optional)

The same process as adding a theme, lets say you want to add **quokka-cart** module.

Add the module submodule

```bash
git submodule add https://github.com/quokkaproject/quokka-cart modules/cart
git submodule init
```

Create the mapping

```yaml
    volumes:
        ...
        - ./modules/cart:/quokka/quokka/modules/cart
```

## Run

> NOTE: Only at the first run MongoDB will create its base files under data folder. It may take some minutes to start for the first time, so it is a good idea to warm it up once using the command `docker-compose run mongo` and wait until mongodb creates your structure for the first time, when you see the message **waiting for connections on port 27017** MongoDB is ok! wait some seconds and press CTRL+C Mongo container will shutdown and you can continue to next step.


```bash
docker-compose up -d
```

Access http://localhost:5000

Configure **nginx** or another server to proxy that port.


## updating Quokka CMS

Quokka is added as a git submodule, to update it use

```bash
git submodule update
```
