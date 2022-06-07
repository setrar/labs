## :whale2: Container Tools


## :a: Install  [Docker](https://www.docker.com/)

:desktop_computer: Using `choco` in `Powershell` admin terminal


- [ ] Install Docker Desktop

```
choco install docker-desktop
```


```
docker build . --tag labs-activemq:5.16.2
```


```
docker container run --name activemq -p 8161:8161 -p 61616:61616 -d labs-activemq:5.16.2
```
