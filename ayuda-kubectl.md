# Ayuda Kubernetes
Comandos útiles de Kubernetes

## Minikube

Inicia un clúster de Minikube e instala Calico como CNI (Container Network Interface).
Calico permite definir políticas de red (NetworkPolicy) para controlar tráfico entre namespaces, pods, etc.
```
minikube start --cni=calico
```

## Namespace
Muestra todos los namespaces del cluster
```
kubectl get namespaces
```

## Servicios

Muestra información de los servicios
```
kubectl get services -n monitoring-ana-001
```

Muestra detalle de un servicio
```
kubectl describe service <nombre-del-servicio> -n monitoring-ana-001
```

Crea túnel hasta el servicio dentro del cluster de Minikube
```
minikube service grafana-service -n monitoring-ana-001 --url
```

## ArgoCD

Expone el puerto de ArgoCD para que sea accesible desde fuera del cluster
```
kubectl port-forward svc/argocd-server -n argocd 8080:443
```


## Vagrant
túnel ssh
```
vagrant ssh -- -L 8080:127.0.0.1:8080 -L 3000:127.0.0.1:3000 -L 5000:127.0.0.1:5000
```
8080 -> ArgoCD
3000 -> Gitea
5000 -> Checkmk

# Port Forwarding de los servicios
```
kubectl port-forward svc/argocd-server -n argocd 8080:443 --address 0.0.0.0

kubectl port-forward svc/gitea -n gitea 3000:3000

kubectl port-forward svc/checkmk -n checkmk 5000:5000
```
