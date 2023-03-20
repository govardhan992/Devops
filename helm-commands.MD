# Add stable to helm

```sh
helm repo add stable https://charts.helm.sh/stable
helm search repo <chartname>

helm install repo stable/<chartname> <releasename>
  
helm pull <chartname>
  
helm package <chartname>

helm uninstall RELEASE_NAME
```
