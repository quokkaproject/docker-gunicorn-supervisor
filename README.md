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
```

## Configure (optional)

It is with the default configurations for running, but you can change configs editing **docker-compose.yml** file.

Normally you will expose this service using a server like **nginx**, by default it runs using 5000 port, you change the port mapping in docker-compose.yml

```yaml

    ports:
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

```bash
docker-compose build
docker-compose up -d
```

Access http://localhost:5000

Configure **nginx** or another server to proxy that port.


## updating Quokka CMS

Quokka is added as a git submodule, to update it use

```bash
git submodule update
```
