# :cat2: Tomcat



```
docker build -t labs/tomcat-8:8.5.79 . 
```

```
docker image ls
```


```
docker container run --interactive --tty --detach --name some-tomcat --publish 8088:8080 labs/tomcat-8:8.5.79
```


```
docker container rm -f some-tomcat
```
 
 
```
docker image rm labs/tomcat-8:8.5.79
```
