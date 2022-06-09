# Part :two: :heavy_plus_sign: CONFIGURING STANDARD ACTIVEMQ COMPONENTS

```
export LABS=${HOME}/Developer/labs
```

```
export ACTIVEMQ_HOME=${HOME}/Developer/labs/mom/binary/apache-activemq-5.16.2
```


```
nano ${ACTIVEMQ_HOME}/conf/activemq.xml
```


| Parts                | Chapters                  | Descriptions                                                         | Available |
|----------------------|---------------------------|:---------------------------------------------------------------------|-----------|
| [Part :two:](.)  |                               | :heavy_plus_sign: CONFIGURING STANDARD ACTIVEMQ COMPONENTS           |
|                      | [`ch`:four: ](ch4)        | :heavy_minus_sign: Connecting to ActiveMQ                            | :point_left: | 
|                      | [`ch`:five: ](ch5)        | :heavy_minus_sign: ActiveMQ message storage                          |
|                      | [`ch`:six: ](ch6)         | :heavy_minus_sign: Securing ActiveMQ                                 |


## Chapter :four:

- [ ] Create the `ch4` Maven Project using the below command

```
mvn archetype:generate \
    -DgroupId=org.apache.activemq.book.ch4 \
    -DartifactId=ch4 \
    -DarchetypeArtifactId=maven-archetype-quickstart \
    -DarchetypeVersion=1.4 \
    -DinteractiveMode=false
```
- [ ] Navigate to the `ch4` folder

```
cd ch4
```


# [:back: ](../README.md) Return to labs
