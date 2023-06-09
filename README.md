# docker-workflow

a set of docker container management rules for developers

## Prerequisites

- [Docker](https://docs.docker.com/install/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Directory Structure

```
/home/username
├── /projects
│   ├── /project1
│   │   ├── /docker
│   │   │   ├── docker-compose.yml
│   │   ├── /web
│   │   ├── /dump
│   ├── /project2
│   │   ├── /docker
│   │   │   ├── docker-compose.yml
│   │   ├── /web
│   │   ├── /dump
```

Create a main folder for your projects, for example: `/home/username/Projects`. Inside this folder, create a folder for each project, for example: `/home/username/Projects/project1`. Inside each project folder, create a folder called `docker` and inside this folder create a file called `docker-compose.yml`. This file will contain the rules for the docker containers of your project.

The `web` folder will contain the files of your project, for example: `/home/username/Projects/project1/web`. \
The `dump` folder will contain the database dump files, for example: `/home/username/Projects/project1/dump`.

> You can add more folders to your projects, for example: `/home/username/Projects/project1/logs` or `/home/username/Projects/project1/config`.

---

## Aliases

When you open your IDE the integrated terminal will be in the root folder of your project, for example: `/home/username/Projects/project1`.
To prevent CD to the `docker` folder every time you want to perform action to your project, you can add these aliases to your `.bashrc` file.

```sh
# To start containers
alias dup="docker-compose --file ../docker/docker-compose.yml up -d --build"

# To stop containers
alias ddown="docker-compose --file ../docker/docker-compose.yml down --remove-orphans"

# To restart containers
alias dres="ddown && dup"

# To enter in bash
alias dbash="clear && docker-compose --file ../docker/docker-compose.yml exec -itu www-data -w /var/www/html web bash"

# To display logs
alias dlogs="docker-compose --file ../docker/docker-compose.yml logs -f --tail=100"

# To start the container and enter in bash
alias ddev="dup && dbash"
```