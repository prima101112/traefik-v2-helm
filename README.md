# Helm chart for traefik v2 installation without CRD

for official helm chart please refer to [this link](https://github.com/traefik/traefik-helm-chart)

this is helm chart for install traefik v2 that just works
- using config map as static config with default provider file also in same config map
- edit the config map to chnage providers
- using sha256sum of configmap file to always rollout deployment when configmap changes

## How To use
once again *this chart is not official*

1. Clone the repo 
2. Edit the value.yaml like you wish 
3. install from inside the folder
```
helm install traefik-v2 .
```

### to update config
1. edit config in value.yaml
2. upgrade from inside the folder
```
helm upgrade traefik-v2 .
```

## Your dashboard should show up
```
kubectl get svc --namespace default traefik-v2-helm --template "{{ range (index .status.loadBalancer.ingress 0) }}{{.}}{{ end }}"
```
you will get SERVICE_IP (default is load balancer)

open in browser
```
http://SERVICE_IP:8080/dashboard/
```

### note
when trying in minikube make sure you run `minikube tunnel`