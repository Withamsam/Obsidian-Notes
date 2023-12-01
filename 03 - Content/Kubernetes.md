---
creation date: July 20th 2023
last modified date: July 20th 2023
aliases: []
tags: #📕
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #📕  

# [[Kubernetes]]  
___

## Description:  



## Enumerating
[[kubectl]] = Tool that can interact with the API


### Getting information from running services
- Can be found under `env` they startup their own internal server
```bash
$ env
KUBERNETES_SERVICE_PORT=443
KUBERNETES_PORT=tcp://10.96.0.1:443
HOSTNAME=syringe-79b66d66d7-6xdjz
GRAFANA_PORT_3000_TCP_ADDR=10.105.120.1
SHLVL=1
HOME=/home/challenge
OLDPWD=/
GRAFANA_PORT_3000_TCP_PORT=3000
GRAFANA_PORT_3000_TCP_PROTO=tcp
SYRINGE_PORT_3000_TCP_ADDR=10.103.9.166
SYRINGE_PORT_3000_TCP_PORT=3000
SYRINGE_PORT_3000_TCP_PROTO=tcp
GRAFANA_PORT_3000_TCP=tcp://10.105.120.1:3000
_=json
GRAFANA_SERVICE_HOST=10.105.120.1
KUBERNETES_PORT_443_TCP_ADDR=10.96.0.1
PATH=/usr/local/go/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
KUBERNETES_PORT_443_TCP_PORT=443
SYRINGE_PORT_3000_TCP=tcp://10.103.9.166:3000
KUBERNETES_PORT_443_TCP_PROTO=tcp
GRAFANA_PORT=tcp://10.105.120.1:3000
SYRINGE_SERVICE_HOST=10.103.9.166
GRAFANA_SERVICE_PORT=3000
KUBERNETES_SERVICE_PORT_HTTPS=443
SYRINGE_PORT=tcp://10.103.9.166:3000
KUBERNETES_PORT_443_TCP=tcp://10.96.0.1:443
SYRINGE_SERVICE_PORT=3000
PWD=/tmp
KUBERNETES_SERVICE_HOST=10.96.0.1
GOLANG_VERSION=1.15.7
```

- Using [[Curl]] we can check them out for anything interesting: (We are checking against `GRAFANA` from above)
```bash
curl http://10.105.120.1:3000
```
- Running blank like this can show possible subdirectories but we need to check those subdirectories for further information
- If we find a running service under one of these try to find a version of it and search for vulns


### Service Token
```bash
/var/run/secrets/kubernetes.io/serviceaccount/token
```
- Can be used to access other accounts which might have more permissions.
- If we find access to a token here we can use the following to check its permission with [[kubectl]]
```bash
./kubectl auth can-i --list --token='<TOKEN>'
```

___

## Resources:

| Hyperlink                                                                                   | Info |
| ------------------------------------------------------------------------------------------- | ---- |
| [cURL Kubernetes](https://nieldw.medium.com/curling-the-kubernetes-api-server-d7675cfc398c) | This article goes over how we can interact with the API via curl     |


Created Date: July 20th 2023 (07:07 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>
