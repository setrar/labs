# Chapter :one::four: :heavy_minus_sign: Administering and monitoring ActiveMQ



- [ ] ActiveMQ Status

```
${ACTIVEMQ_HOME}/bin/activemq status
```

```
ps | grep `cat ${ACTIVEMQ_HOME}/data/activemq.pid` 
```

:warning: `git bash` Terminal has a `ps -o` issue where `status` command is not working

```
ps: unknown option -- o
Try `ps --help' for more information.
ActiveMQ not running
```


- [ ] ActiveMQ PID 

```
```

- [ ] Log Files

```
tail -f ${ACTIVEMQ_HOME}/data/activemq.log 
```


# References

- [ ] [JMX](https://activemq.apache.org/jmx)
