# ${HOME}/.bashrc


```
cat $HOME/.bashrc
```
 
 
```
# Environment variable must be set after installing the activemq binary
export ACTIVEMQ_HOME=${HOME}/Developer/labs/mom/binary/apache-activemq-5.16.2 

```

```
#THIS MUST BE AT THE END OF THE FILE FOR SDKMAN TO WORK!!!
export SDKMAN_DIR="$HOME/.sdkman"
[[ -s "$HOME/.sdkman/bin/sdkman-init.sh" ]] && source "$HOME/.sdkman/bin/sdkman-init.sh" 
```
