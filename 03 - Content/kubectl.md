---
creation date: July 20th 2023
last modified date: July 20th 2023
aliases: []
tags: #🧰
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #🧰  

# [[kubectl]]  
___

## Description:


## Installation
[Link To Install](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-kubectl-binary-with-curl-on-linux)

## Commands
- If we see **Forbidden** after any command it means current user doesn't have permission to access that 
- Some interesting Kubernetes objects to look for would be `nodes`,  `deployments`, `services`, `ingress`, `jobs`
	- But we don't always have access to these depending on permissions
- Checking `env` is a good way to locate running [[Kubernetes]] pods

### Checking Current User Permission
```bash
./kubectl auth can-i --list
```

Results Example:
```bash
Resources                                       Non-Resource URLs                     Resource Names   Verbs
*.*                                             []                                    []               [*]
                                                [*]                                   []               [*]
selfsubjectaccessreviews.authorization.k8s.io   []                                    []               [create]
selfsubjectrulesreviews.authorization.k8s.io    []                                    []               [create]
                                                [/.well-known/openid-configuration]   []               [get]
                                                [/api/*]                              []               [get]
                                                [/api]                                []               [get]
                                                [/apis/*]                             []               [get]
                                                [/apis]                               []               [get]
                                                [/healthz]                            []               [get]
                                                [/healthz]                            []               [get]
                                                [/livez]                              []               [get]
                                                [/livez]                              []               [get]
                                                [/openapi/*]                          []               [get]
                                                [/openapi]                            []               [get]
                                                [/openid/v1/jwks]                     []               [get]
                                                [/readyz]                             []               [get]
                                                [/readyz]                             []               [get]
                                                [/version/]                           []               [get]
                                                [/version/]                           []               [get]
                                                [/version]                            []               [get]
                                                [/version]                            []               [get]
```
- If we find `*.*` with a verb of `*` this means this is a cluster admin account



### Interacting with Resources
#### Listing 
```bash
./kubectl get secrets
```

Example:
```bash
NAME                    TYPE                                  DATA   AGE
default-token-8q4vp     kubernetes.io/service-account-token   3      140d
developer-token-rnmqz   kubernetes.io/service-account-token   3      140d
secretflag              Opaque                                1      140d
syringe-token-6w8tq     kubernetes.io/service-account-token   3      140d
```

#### Listing Data
```bash
./kubectl get secrets secretflag -o 'json'
```

Example: 
```bash
{
    "apiVersion": "v1",
    "data": {
        "flag": "ZmxhZ3tkZjJhNjM2ZGUxNTEwOGE0ZGM0MTEzNWQ5MzBkOGVjMX0="
    },
    "kind": "Secret",
    "metadata": {
        "annotations": {
            "kubectl.kubernetes.io/last-applied-configuration": "{\"apiVersion\":\"v1\",\"data\":{\"flag\":\"ZmxhZ3tkZjJhNjM2ZGUxNTEwOGE0ZGM0MTEzNWQ5MzBkOGVjMX0=\"},\"kind\":\"Secret\",\"metadata\":{\"annotations\":{},\"name\":\"secretflag\",\"namespace\":\"default\"},\"type\":\"Opaque\"}\n"
        },
        "creationTimestamp": "2023-03-02T23:51:30Z",
        "name": "secretflag",
        "namespace": "default",
        "resourceVersion": "819",
        "uid": "f341b287-9f62-41c2-9eac-4d1a27ad76dc"
    },
    "type": "Opaque"
}
```


### Getting a Shell in a Pod
1. If we have access to an accounts token we can use that to spawn a shell as that user
2. Start by checking pods
```bash
./kubectl get pods --token='<TOKEN>'
```

Example:
```bash
NAME                       READY   STATUS    RESTARTS       AGE
grafana-57454c95cb-f9js5   1/1     Running   2 (140d ago)   140d
syringe-79b66d66d7-6xdjz   1/1     Running   2 (140d ago)   140d
```

3. Next we will execute a command as a user requesting a bash session: (We will use **grafana-57454c95cb-f9js5** in example)
```bash
./kubectl exec -it <NAME> --token='<TOKEN>' -- /bin/bash
```

Example:
```bash
./kubectl exec -it grafana-57454c95cb-f9js5 --token=eyJhbGciOiJSUzI1NiIsImtpZCI6IkpwcUhIZ1hyRF9FbGYyQ1piWHNiemZhNGpnSTl0Z3Z1X2dMeFAtTURUaVUifQ.eyJhdWQiOlsiaHR0cHM6Ly9rdWJlcm5ldGVzLmRlZmF1bHQuc3ZjLmNsdXN0ZXIubG9jYWwiXSwiZXhwIjoxNzIxNDM4MTgzLCJpYXQiOjE2ODk5MDIxODMsImlzcyI6Imh0dHBzOi8va3ViZXJuZXRlcy5kZWZhdWx0LnN2Yy5jbHVzdGVyLmxvY2FsIiwia3ViZXJuZXRlcy5pbyI6eyJuYW1lc3BhY2UiOiJkZWZhdWx0IiwicG9kIjp7Im5hbWUiOiJncmFmYW5hLTU3NDU0Yzk1Y2ItZjlqczUiLCJ1aWQiOiI4N2RiNDhiMC1kMTc2LTQyOGMtOWZhNS0yZDVkMzlmMjU4NjcifSwic2VydmljZWFjY291bnQiOnsibmFtZSI6ImRldmVsb3BlciIsInVpZCI6ImIwMWIwODc5LWNlMDItNDAxNC1iNjEyLTEyOWVlYzAxNjdiNCJ9LCJ3YXJuYWZ0ZXIiOjE2ODk5MDU3OTB9LCJuYmYiOjE2ODk5MDIxODMsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDpkZWZhdWx0OmRldmVsb3BlciJ9.QJzCZk4ORuKSht3vIXEmqvgktnTtAxi_oGPGYQZepE-afTIlKq98H9HuxquuRF68dZ0mMcpudIDHMRUf1umpXbvJ2-C6QatJ7mBHQo8pj0O99GUcBzqLFaWzvznTizxSSa8U4cFOmX5_yjV0dqHtxddMyrHZ7Maavhtyj_HJt6JrXOYzcIoqMuuodW7iKcJ2e1kKqfllUKoynWjUCrmb1z4PZ7IDaQGK3Ksw7JhRYRpOtaYeHLNV8bHw_WQppZ0BS7KkZ8RMIzu_WH8ZhfDnGCfaa41lM77KF0CRs4u8YWMd6P4-TpvNcMhjIusq0Cr9k72U2PGN3uVv05ZI0cKLZQ -- /bin/bash
```

4. Success verify new user with a `whoami`






___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: July 20th 2023 (07:40 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>
