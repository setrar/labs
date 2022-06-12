# :cat2: Tomcat



```
docker build -t labs/tomcat-8:8.5.79 . 
```

```
docker image ls
```


```
docker container run --name some-tomcat --publish 8088:8080 --detach labs/tomcat-8:8.5.79
```


```
docker container rm -f some-tomcat
```
 
 
```
docker image rm labs/tomcat-8:8.5.79
```

http://localhost:8088/SampleWebApp/ 

# References

- [ ] [Docker Tomcat Example – Dockerfile for Tomcat, Docker Tomcat Image](https://www.middlewareinventory.com/blog/docker-tomcat-example-dockerfile-sample)
