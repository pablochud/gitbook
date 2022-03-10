## Podstawowe komendy ##
##### Budowanie obrazu #####
z katalogu, w którym znajduję się Dockerfile
`docker build -t <imagename> .`
##### Lista obrazów #####
`docker image ls`
albo zależne od wersji Dockera
`docker images`
##### Uruchamianie kontenera #####
_uruchamianie kontenera odbywa się przy pomocy komendy `run`_.
_Poniżej przykłady użycia:_
`docker run -p 4000:80 <imagename>`
`docker run --name <containername> -p 80:80 <imagename>`
`docker run --name <contname> --link some-redis:redis -d -p 80:80 <imgname>`
##### Uruchamianie kontenera w trybie interactive #####
`docker run --rm -it -p 4000:80 <imgname> bash`
`docker exec -it <containerIDorName> bash`

##### Zapisywanie stanu kontenera jako osobny obraz #####
`docker commit <containerIDorName> <imagename>`

## Zarządzanie serwisami, czyli STACK ##
Na przykładzie `docker-compose.yml`
```
version: "3"
services:
  web:
    # replace username/repo:tag with your name and image details
    image: username/repo:tag
    deploy:
      replicas: 5
      resources:
        limits:
          cpus: "0.1"
          memory: 50M
      restart_policy:
        condition: on-failure
    ports:
      - "80:80"
    networks:
      - webnet
networks:
  webnet:
```
##### Uruchamianie load-balancera #####
`docker swarm init`
##### Uruchamianie stack'a i nadanie nazwy aplikacji #####
`docker stack deploy -c docker-compose.yml <appname>`
##### Lista serwisów #####
`docker service ls`
Pojedyńcze kontenery uruchomione w serwisie, nazywają się taskami.
##### Lista tasków #####
`docker service ps <appname>_web`
Lista tasków powinna również znajdować się na głównej liście kontenerów
##### Usuwanie stacka i swarm'a #####
`docker stack rm <appname>`
`docker swarm leave --force`
