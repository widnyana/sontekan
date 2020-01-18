# KUBECTL


## attach ke pod dengan > 1 container di dalamnya:


```kubectl exec <POD NAME> -c <CONTAINER NAME> -- <COMMAND>```

sample:

```kubectl exec mc1 -c 1st -- sh```
