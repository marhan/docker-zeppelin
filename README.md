# Docker based Zeppelin

Dockerized and preconfigured [Zeppelin](https://zeppelin.apache.org/docs/0.8.1/setup/deployment/docker.html). 
This project is meant to be a sandbox to learn Zeppelin and Spark. 
The applications are operated with Docker, so that the student does not have to deal with the partly complex technical dependencies. 
The goal is to enable a quick start into the technology.  

## Introduction

[Apache Zeppelin](http://zeppelin.apache.org/) is a Web-based notebook that enables data-driven, 
interactive data analytics and collaborative documents with SQL, Scala and more. 
The Zeppelin Notebooks make strong use of [Apache Spark](https://spark.apache.org), which is a fast and general engine for large-scale data processing. 
The Spark functions itself require for various tasks [Apache Hadoop](https://hadoop.apache.org/), which is a open-source software for reliable, scalable, distributed computing.

The Zeppelin Notebooks are placed in a separated [repository](https://github.com/marhan/zeppelin-notebook-samples) and are integrated as a Git submodule.

[Presentation slides can be found here](https://speakerdeck.com/markushanses/apache-zeppelin-tutorial)

## Used versions

- Zeppelin version = 0.8.1
- Spark version = 2.4.3
- Hadoop version = 2.8.5

## Requirements

### Software
- Docker
- Docker Compose

### Hardware (complete stack)
- RAM = 5GB

### Hardware (zeppelin only)  
- RAM = 2GB

## Checkout

    git clone https://github.com/marhan/docker-zeppelin-tutorial.git
    git clone https://github.com/marhan/zeppelin-notebook-samples.git docker-zeppelin-tutorial/zeppelin/notebook
    
## Start complete stack

    docker-zeppelin-tutorial
    docker-compose up -d
    
## WebUIs

* [Zeppelin](http://localhost:10000) 
* [Adminer (Postgres)](http://localhost:10002) 
    * PostgreSQL
        * System: PostgreSQL
        * Server: postgresdb
        * Username: zeppelin_admin
        * Password: zeppelin_admin
        * Database: zeppelin
    * MariaDB
        * System: MySQL
        * Server: mariadb
        * Username: root
        * Password: zeppelin
        * Database: zeppelin
* [Webdav Web Server](http://localhost:10003) 
    * Username: zeppelin
    * Password: zeppelin
* [Minio Cloud Storage Server](http://localhost:10004)
    * Access Key: zeppelin
    * Secret Key: zeppelin 

## Source of data used in notebooks

- [London population](https://github.com/datasets/london-population)
- [Bank data](http://repositorium.sdum.uminho.pt/handle/1822/14838)
- [Spark examples](https://github.com/apache/spark/tree/master/examples/src/main/resources)
    
## Pulled Docker Images

- [Zeppelin](https://hub.docker.com/r/apache/zeppelin)
- [Postgres](https://hub.docker.com/_/postgres)
- [MariaDB](https://hub.docker.com/_/mariadb)
- [Adminer](https://hub.docker.com/_/adminer/)
- [Minio](https://hub.docker.com/r/minio/minio/)
- [WebDAV](https://hub.docker.com/r/bytemark/webdav/)

## Development

### Docker Compose CLI

#### Recreate zeppelin image and container
    
    docker-compose rm -f -s -v zeppelin
    docker rmi zeppelin    
    docker-compose up --force-recreate zeppelin
    
#### Remove all containers and volumes

    docker-compose stop
    docker-compose rm -f -v
    
#### Bash into a running container

    docker-compose exec zeppelin bash
    
### Docker CLI

#### Show running containers

    docker ps # all
    docker ps --format '{{.Names}}' # names only
    
#### Delete all containers

    docker rm $(docker ps -a -q)
    
#### Delete all images

    docker rmi $(docker images -q)
    
### Git Submodule

In repository root folder you can execute the command below.

    git submodule add git@github.com:marhan/zeppelin-notebook-samples.git zeppelin/notebook
    
This will create the file `.gitmodule` with the entry below. 

    [submodule "zeppelin/notebook"]
	    path = zeppelin/notebook
	    url = git@github.com:marhan/zeppelin-notebook-samples.git
