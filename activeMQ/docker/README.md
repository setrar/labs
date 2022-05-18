# Docker

- [ ] Build

```
docker build . --tag temp-activemq:5.16.0 
```

- [ ] Run

```
docker container run --name activemq --publish 8161:8161 --publish 61616:61616 --detach temp-activemq:5.16.0 
```

# References

- [ ] [freekode/docker-activemq](https://github.com/freekode/docker-activemq)
- [ ] [Not able to access admin console for an activemq instance running in a docker container](https://stackoverflow.com/questions/63127321/not-able-to-access-admin-console-for-an-activemq-instance-running-in-a-docker-co)
