# :whale2: Container Tools


## :a: Install  [Docker](https://www.docker.com/)

:desktop_computer: Using `choco` in `Powershell` admin terminal


- [ ] Install Docker Desktop

```
choco install docker-desktop
```

- [ ] Build the ActiveMQ image


```
docker image build --tag labs/activemq:5.16.2 .
```

- [ ] Run the ActiveMQ container

```
docker container run --name some-activemq --publish 7161:8161 --publish 7616:61616 --detach labs/activemq:5.16.2 
```

- [ ] Connect to ActiveMQ Web Console

http://localhost:7161/admin/


User: `admin`

Pwd: `admin`

# References

- [ ] [freekode/docker-activemq](https://github.com/freekode/docker-activemq)
- [ ] [Not able to access admin console for an activemq instance running in a docker container](https://stackoverflow.com/questions/63127321/not-able-to-access-admin-console-for-an-activemq-instance-running-in-a-docker-co)
- [ ] [Watch command for Git Bash](https://gist.github.com/espaciomore/28e24ce4f91177c0964f4f67bb5c5fda)
- [ ] [Deploying Active-MQ in a Kubernetes cluster](https://medium.com/zolo-engineering/deploying-active-mq-in-a-kubernetes-cluster-3674f4fd6210)
