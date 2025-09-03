# 📘 Kubectl Cheat Sheet – Most Important Commands

## 🔹 Cluster Info
```sh
kubectl version --short             # Show client and server versions
kubectl cluster-info                # Display cluster master and services
kubectl get componentstatuses       # Check cluster component health
kubectl config view --minify | grep name: # Show current context
kubectl config current-context      # Get current context
```

---

## 🔹 Namespaces
```sh
kubectl get namespaces              # List all namespaces
kubectl create namespace <name>     # Create a namespace
kubectl delete namespace <name>     # Delete a namespace
kubectl config set-context --current --namespace=<name> # Switch namespace
```

---

## 🔹 Pods
```sh
kubectl get pods                    # List all pods
kubectl get pods -o wide            # List pods with more details
kubectl describe pod <pod_name>     # Show detailed info about a pod
kubectl logs <pod_name>             # View pod logs
kubectl exec -it <pod_name> -- /bin/sh   # Open shell inside pod
kubectl delete pod <pod_name>       # Delete a pod
```

---

## 🔹 Deployments
```sh
kubectl get deployments             # List deployments
kubectl describe deployment <name>  # Show details about deployment
kubectl create deployment <name> --image=<image>   # Create deployment
kubectl scale deployment <name> --replicas=3       # Scale deployment
kubectl rollout status deployment/<name>          # Check rollout status
kubectl rollout undo deployment/<name>            # Rollback deployment
kubectl delete deployment <name>   # Delete deployment
```

---

## 🔹 Services
```sh
kubectl get services                # List all services
kubectl describe service <name>     # Show service details
kubectl expose pod <pod_name> --port=80 --target-port=8080 # Expose pod
kubectl expose deployment <name> --type=LoadBalancer --port=80 # Expose deployment
kubectl delete service <name>       # Delete service
```

---

## 🔹 ConfigMaps & Secrets
```sh
kubectl get configmaps              # List ConfigMaps
kubectl describe configmap <name>   # Describe ConfigMap
kubectl create configmap <name> --from-literal=key=value # Create ConfigMap

kubectl get secrets                 # List secrets
kubectl describe secret <name>      # Describe secret
kubectl create secret generic <name> --from-literal=user=admin --from-literal=pwd=1234 # Create secret
```

---

## 🔹 Nodes
```sh
kubectl get nodes                   # List all nodes
kubectl describe node <name>        # Node details
kubectl cordon <node_name>          # Mark node unschedulable
kubectl drain <node_name>           # Drain node (evict pods)
kubectl uncordon <node_name>        # Mark node schedulable
```

---

## 🔹 Apply & Delete Resources
```sh
kubectl apply -f <file>.yaml        # Apply resource from YAML file
kubectl delete -f <file>.yaml       # Delete resource from YAML file
kubectl get all                     # List all resources in namespace
```

---

## 🔹 Debugging & Troubleshooting
```sh
kubectl describe <resource_type> <name>   # Describe resource
kubectl logs <pod_name>                   # Check logs
kubectl logs <pod_name> -c <container>    # Logs for specific container
kubectl exec -it <pod_name> -- sh         # Get shell access
kubectl top pod                           # Show resource usage of pods
kubectl top node                          # Show resource usage of nodes
```

---

## 🔹 Shortcuts / Aliases
```sh
kubectl get po          # pods
kubectl get deploy      # deployments
kubectl get svc         # services
kubectl get ns          # namespaces
```