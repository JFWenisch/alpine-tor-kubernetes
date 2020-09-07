#alpine tor kubernetes
Class kubernetes deployment for  [alpine-tor-docker](https://github.com/JFWenisch/alpine-tor-docker)
For helm deployments pls refer to  [alpine-tor-helm](https://github.com/JFWenisch/alpine-tor-helm)

## Kubernetes deployment

  

### Create kubernetes deployment

The alpine-tor-${mode}.yaml can be used to create an deployment which ensures 1 running running pod and uses a service to exposes the needed ports.
Supported modes: proxy,exit,middle,bridge. For more information on supported modes pls refer to the [alpine-tor-docker readme](https://github.com/JFWenisch/alpine-tor-docker) and the official [tor-relay-guide](https://trac.torproject.org/projects/tor/wiki/TorRelayGuide)
The different modes these can be set via --set mode=$value. If no mode is specified the default value "mode:proxy" will be used.



To create the service and deployment run

  

```

kubectl create -f alpine-tor-${mode}.yaml

```

The result should look like

  

```

service/alpine-tor-service created

deployment.apps/alpine-tor created

```

  

In order to be able to connect to the socks proxy you'll need to note down the automatically assigned port. Run the below command to view the ports

  

```

kubectl get service alpine-tor-service

```

  

Which should look like

```

NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE

alpine-tor-service NodePort 10.152.183.117 <none> 9050:30848/TCP 82s

```

  

You can test the proxy by running

```

curl -x socks5h://${ExternalNodeIP}:30848 -L http://ifconfig.me

```

  

### Delete kubernetes deployment

```

kubectl delete -f alpine-tor-deployment.yaml

```


## Further information

[alpine-tor-docker](https://github.com/JFWenisch/alpine-tor-docker)

[Tor Project](https://www.torproject.org/)

[Alpine Linux ](https://alpinelinux.org/)
