# Plan4BA Infrastructure
##Requirements
- install docker
- install maven (mvn)(only for building)
- install git(only for building)
## Build from Source
### CachingService:
```
git clone https://github.com/Plan4BA/CachingService
cd CachingService
mvn clean package
docker build -t plan4ba/cachingservice .
```
### Loginservice:
```
git clone https://github.com/Plan4BA/Loginservice
cd Loginservice
mvn clean package
docker build -t plan4ba/loginservice .
```
### DBService:
```
git clone https://github.com/Plan4BA/DBService
cd DBService
mvn clean package
docker build -t plan4ba/dbservice .
```
### Webservice:
```
git clone https://github.com/Plan4BA/Webservice
cd Webservice
mvn clean package
docker build -t plan4ba/webservice .
```

## Deployment
### Networks
```
docker network create database
docker network create backend
docker network create frontend
```

### Management-Container
### Portainer (see https://portainer.io/install.html)
```
docker volume create portainer_data
docker run --rm -d --name portainer -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
```
### PostgreSQL
```
docker run --rm --name postgres --net database --net-alias database -e POSTGRES_PASSWORD=dbservice -e POSTGRES_USER=dbservice -e POSTGRES_DB=dbservice -d postgres
```
### Plan4BA-Container
#### DBService
```
docker run -d --rm --name dbservice --net database -e DATABASE_DRIVER=postgresql -e DATABASE_HOST=database -e DATABASE_PORT=5432 -e DATABASE_NAME=dbservice -e DATABASE_PASSWORD=dbservice -e DATABASE_USER=dbservice plan4ba/dbservice
docker network connect backend dbservice
```
#### Loginservice
```
docker run -d --rm --name loginservice --net backend --net-alias loginservice plan4ba/loginservice
```
#### Cachingservice
```
 docker run -d --rm --name cachingservice --net backend --net-alias cachingservice -e DBSERVICE_ENDPOINT=http://dbservice:8080 -e MAX_PARALLEL_JOBS=5 -e TIMESPAN_START=23:00 -e TIMESPAN_END=02:00 plan4ba/cachingservice
```
#### Webservice
```
docker run -d --rm --name webservice --net backend --net-alias webservice -p 8080:8080 -e DBSERVICE_ENDPOINT=http://dbservice:8080 -e CACHINGSERVICE_ENDPOINT=http://cachingservice:8080 -e LOGINSERVICE_ENDPOINT=http://loginservice:8080 -e ENABLE_SWAGGER=false plan4ba/webservice
docker network connect frontend webservice
```



