# Befehle

`kubectl --kubeconfig kubeconfig-admin.conf --insecure-skip-tls-verify=true get al`

`kubectl --kubeconfig=./kubeconfig-admin --insecure-skip-tls-verify=true get all -A`

`kubectl --kubeconfig=./kubeconfig-admin --insecure-skip-tls-verify=true create namespace laura-dubach`

https://kubernetes.io/docs/tutorials/kubernetes-basics/deploy-app/deploy-intro/#kubectl-basics


# Grundsyntax von kubectl Kommandos

`kubectl [befehl] [TYP] [NAME] [flags]`

wobei befehl, TYP, NAME und flags Folgendes sein können:

- befehl: Gibt die Operation an, die Sie an einer oder mehreren Ressourcen durchführen möchten, zum Beispiel create, get, describe, delete.

- TYP: Gibt den Ressourcentyp an. Ressourcentypen sind nicht case-sensitive und Sie können die Singular-, Plural- oder abgekürzte Form angeben. Die folgenden Befehle erzeugen beispielsweise dieselbe Ausgabe:

```
kubectl get pod pod1  
kubectl get pods pod1  
kubectl get po pod1
```
- NAME: Gibt den Namen der Ressource an. Bei Namen wird zwischen Gross- und Kleinschreibung unterschieden. Wenn der Name weggelassen wird, werden Details für alle Ressourcen mit dem Typen TYP angezeigt, zum Beispiel kubectl get pods.

- flags: Gibt optionale Flags an. Sie können beispielsweise die Flags -n oder --namespace verwenden, um in einem anderen Namespace zu handeln.

# Container Starten mit kubectl run
Um einen Container zu starten müssen wir einen Pod erstellen.

Als Platzhalter- oder Beispiel-Applikation verwenden wir diesmal Podinfo. Das hat den Vorteil eines knuffigen Maskott--ich mach nur Witze. Diese Applikation zeigt unter anderem an, wie der Pod heisst, der gerade antwortet. Damit können wir ein paar

`kubectl run kubectl-run-test --image=stefanprodan/podinfo:6.9.1 --port=9898`

Okay, was jetzt?? Mit dem nächsten Kommando können wir einen Port von unserem Rechner bis zu einem Pod durchschleusen:

# Port durchschleusen mit kubectl port-forward

`kubectl port-forward pods/kubectl-run-test 8000:9898`

Der Port links vom Doppelpunkt ist lokal, der Port rechts davon ist am Pod. Das heisst wir können jetzt mit dem Browser darauf zugreifen. Der Hostname ist http://localhost und der Port ist 8000.