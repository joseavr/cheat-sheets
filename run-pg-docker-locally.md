---
authors:
  - Jose Valdivia
title: Set up Postgres in Docker Locally
description: A deep dive on how to create a CI/CD pipeline.
date: 2024-10-18
image: /content/github-actions.webp
tags:
  - architecture
---

Easy way to run postgres locally for a testing database.

## First way

> Testing Database installation in Docker guide- [here](https://orm.drizzle.team/docs/guides/postgresql-local-setup)



## Second way

#### Create docker file

Copy and paste the following in the root of your project directory.


```yml showHeader filename="docker-compose.yml"
services:
  db:
    image: postgres:16.2
    environment:
      - POSTGRES_PASSWORD=${DB_PASSWORD}
      - POSTGRES_USER=${DB_USER}
      - POSTGRES_DB=${DB_NAME}
    ports:
      - ${DB_PORT}:5432
    volumes:
      - ./db-data:/var/lib/postgresql/data
```

#### Set Environment Variables


```.env
DB_HOST=

DB_USER=

DB_PASSWORD=

DB_NAME=

DB_PORT=

DATABASE_URL=postgresql://${DB_USER}:${DB_PASSWORD}@${DB_HOST}:${DB_PORT}/${DB_NAME}
```

  
#### Run

Run the docker with this command

```bash
docker compose up
```


#### To remove a container

```bash
rm -rf db-data
```


## Third way

[Reference](https://www.youtube.com/watch?v=yW6HnMUAWNU&list=PL2QTGA7CZZ5HRvxDhI0uZ8k-_7Se4RnLx&index=4) 

Create a docker-compose.yml
```yaml
version: '3'
services:
	db:
		image: postgres
		restart: always
		volumes:
			- ./data/db:/var/lib/postgresql/data
		ports:
			- 5432:5432
		environment:
			- POSTGRES_DB=testDB
			- POSTGRES_USER=postgres
			- POSTGRES_PASSWORD=postgres
	## GUI
	adminer:
		image: adminer
		restart: always
		ports:
			- 8080:8080
```

Run docker

```bash
docker compose up
```


Open localhost:8080 to open the adminer GUI. Then, enter credentials