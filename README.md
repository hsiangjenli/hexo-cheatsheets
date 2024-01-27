# Hexo Cheatsheets Theme

A new **cheatsheets** theme for Hexo.
The design is from [devhints](http://devhints.io)

## Installation
### Install manually
```bash
npm install hexo-cli -g
npm install make -g
npm install -g sass
```
### Creating an environment using Docker
```yaml
FROM node:17-alpine

WORKDIR /app
COPY package.json yarn.lock package-lock.json /app/
RUN npm install hexo-cli make sass -g
RUN rm -rf node_modules && npm install --force
RUN set -x \
    && . /etc/os-release \
    && case "$ID" in \
        alpine) \
            apk add --no-cache bash git openssh \
            ;; \
        debian) \
            apt-get update \
            && apt-get -yq install bash git openssh-server \
            && apt-get -yq clean \
            && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
            ;; \
    esac \
    && yarn bin || ( npm install --global yarn && npm cache clean ) \
    && git --version && bash --version && ssh -V && npm -v && node -v && yarn -v

RUN npm audit fix --force
```

## Init project
### Currently dir
```bash
hexo init .
```
### The generated project structure
```yaml
.
├── Dockerfile
├── Makefile
├── README.md
├── _config.yml
├── compose-dev.yaml
├── db.json
├── node_modules
├── package.json
├── scaffolds
├── source
├── themes (You should put your theme in this folder)
│   └── hexo-cheatsheets
└── yarn.lock
```
### cd to `themes`
```bash
cd themes
git clone https://github.com/hsiangjenli/hexo-cheatsheets.git
```

### Modify `theme` setting in `_config.yml` to `hexo-cheatsheets`
### Disable default code `highlight` plugin in `_config.yml`
```yaml
highlight:
  enable: false
```

## Posts format
### Header's meta data
```yaml
---
title: Hello World
date: 2023-02-11 
tags: hello-world
categories: hello-world
version: 0.10
---
...
```

## Reference
1. [glazec/hexo-cheatsheets](https://github.com/glazec/hexo-cheatsheets)
1. [Hexo Cheatsheets Theme](https://www.inevitable.tech/posts/59f1905d/)
1. [rstacruz/cheatsheets](https://github.com/rstacruz/cheatsheets)