# Cluster starten mit HyperV

`minikube start --driver=hyperv --hyperv-virtual-switch "Default Switch"`

# Kubernetes Dashboard starten

`minikube dashboard`

# Deploy ausführen

`kubectl apply -f xxxx.yaml`

# Service öffnen

`minikube service xxxx`

# Cluster stoppen

`minikube stop`

# Cluster löschen

`minikube delete`

# Ingress aktivieren

`minikube addons enable ingress`