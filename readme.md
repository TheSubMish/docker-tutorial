Dockerfile

    create a python image:
        FROM python:3.11-slim-bullseye
        WORKDIR /app
        COPY . /app
        CMD ["python","main.py"]

terminal

    docker build -t image-name:image-version . 
    (-t flag "tag" is used to define tagname of an image)

    docker run -d image-name:imgage-version
    (-d flag "detach" is used run image in background)

    docker ps
    (shows all running containers)

    docker ps -a
    (shows all containers)

    docker stop container-name | docker stop container-id
    (stops runnning container)

    docker start container-name | docker start container-id
    (start stopped container)

    docker logs container-name | docker logs container-id
    (lets you see container's logs)

    docker rm container-name | docker rm container-id
    (delete container)

    docker rmi image-id:latest | docker rmi image-full-tagname:latest 
    (delete latest image)

docker-compose.yml
(lets you work with multiple docker containers)
    version: "3"

    services:
    db:
        image: postgres
        environment:
        POSTGRES_DB : dockerdb
        POSTGRES_USER : postgres
        POSTGRES_PASSWORD : TheSubMish
        POSTGRES_HOST : '127.0.0.1'
        POSTGRES_PORT : 5432
        volumes:
        - postgres_data:/var/lib/postgresql/data

    web:
        build: .
        environment:
        SECRET : project
        command: python manage.py runserver 0.0.0.0:8000
        volumes:
        - .:/code
        ports:
        - "8000:8000"
        depends_on:
        - db

    volumes:
    postgres_data: {}


    docker-compose up
    (run multiple)

    docker-compose down
    (stops all running containers)

    docker exec -it container-id bash | docker exec -it container-name bash
    (execute container in cli)

    psql -h localhost -U postgres
    (opens postgres cli)

    SELECT datname FROM pg_database;
    (shows all database)

    CREATE DATABASE db_name;
    (create database)