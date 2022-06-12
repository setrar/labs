# :cat2: Tomcat



```
docker build --tag labs/tomcat-8:8.5.79 . 
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
- [ ] [Getting java.lang.ClassNotFoundException: org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter](https://stackoverflow.com/questions/56684075/getting-java-lang-classnotfoundexception-org-springframework-web-servlet-mvc-an)
- [ ] [mvc:annotation-driven is not bound](https://stackoverflow.com/questions/6001593/mvcannotation-driven-is-not-bound)
