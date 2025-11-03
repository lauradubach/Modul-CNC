# Cluster mit Kind erstellen

`kind create cluster --config .\kind-config.yaml`

# Push Image to Ducker Hub
 
cd into src folder
 
docker login
 
docker build -t lauradubach/musicfinder:latest -f Dockerfile.prod .
 
docker buildx build -t lauradubach/musicfinder:latest -f Dockerfile.prod .
 
docker push lauradubach/musicfinder:latest

# Ingress Controler installieren

`kubectl apply -f https://kind.sigs.k8s.io/examples/ingress/deploy-ingress-nginx.yaml`