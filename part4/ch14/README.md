# Chapter :one::four: :heavy_minus_sign: Administering and monitoring ActiveMQ



- [ ] [Docker image with ActiveMQ and HawtIO on Alpine Linux.](https://github.com/krizsan/activemq-docker)


- [ ] ActiveMQ Status

```
${ACTIVEMQ_HOME}/bin/activemq status
```


:warning: `git bash` Terminal has a `ps -o` issue where `status` command is not working

```
ps: unknown option -- o
Try `ps --help' for more information.
ActiveMQ not running
```
As a temporary resolution use:


- [ ] ActiveMQ PID 

```
ps | grep `cat ${ACTIVEMQ_HOME}/data/activemq.pid` 
```


- [ ] Log Files

```
tail -f ${ACTIVEMQ_HOME}/data/activemq.log 
```


# References

- [ ] [JMX](https://activemq.apache.org/jmx)
