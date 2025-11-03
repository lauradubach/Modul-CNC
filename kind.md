# 🐳 kind – Schnellstart (deutsche Zusammenfassung)

## 🧩 Cluster erstellen

Ein Kubernetes-Cluster mit *kind* zu erstellen ist ganz einfach:

```bash
kind create cluster
````

* **Standardname:** `kind`
* **Eigenen Namen vergeben:**

  ```bash
  kind create cluster --name mein-cluster
  ```
* **Warten, bis der Cluster bereit ist:**

  ```bash
  kind create cluster --wait 5m
  ```
* **Andere Kubernetes-Version wählen:**

  ```bash
  kind create cluster --image kindest/node:<version>
  ```

*kind* erkennt automatisch **Docker**, **Podman** oder **nerdctl**.
Manuelles Setzen mit:

```bash
export KIND_EXPERIMENTAL_PROVIDER=docker
```

---

## 🧠 Mit dem Cluster interagieren

Nach der Erstellung kannst du mit `kubectl` arbeiten.
Die Konfigurationsdatei liegt standardmäßig unter:

```
~/.kube/config
```

* Eigene Konfiguration beim Erstellen:

  ```bash
  kind create cluster --kubeconfig myconfig.yaml
  ```
* Alle Cluster auflisten:

  ```bash
  kind get clusters
  ```
* Beispiel für Zugriff:

  ```bash
  kubectl cluster-info --context kind-kind
  kubectl cluster-info --context kind-kind-2
  ```

---

## 🗑️ Cluster löschen

Cluster entfernen:

```bash
kind delete cluster
```

Cluster mit Namen löschen:

```bash
kind delete cluster --name mein-cluster
```

> 💡 Wenn der Cluster nicht existiert, wird **kein Fehler** ausgegeben – das ist beabsichtigt.

---

## 📦 Images in Cluster laden

Docker-Images direkt in kind laden:

```bash
kind load docker-image my-app:latest
```

Mehrere Images auf einmal:

```bash
kind load docker-image my-app:latest my-db:latest my-cache:latest
```

Für benannte Cluster:

```bash
kind load docker-image my-app:latest --name test-cluster
```

Image-Archive:

```bash
kind load image-archive /path/to/image.tar
```

**Empfehlungen:**

* Verwende **keinen `:latest` Tag**, um Probleme mit `imagePullPolicy` zu vermeiden.
* Nutze `imagePullPolicy: IfNotPresent` oder `Never`.

---

## 🏗️ Eigene Node-Images bauen

kind nutzt Container als Kubernetes-Nodes.
Du kannst eigene Node-Images erstellen:

```bash
kind build node-image /path/to/kubernetes/source
```

Oder direkt eine Version wählen:

```bash
kind build node-image v1.30.0
kind build node-image --type url https://dl.k8s.io/v1.30.0/kubernetes-server-linux-amd64.tar.gz
```

> ⚠️ Für macOS/Windows: Docker Desktop sollte **mind. 6–8 GB RAM** haben.

---

## ⚙️ Erweiterte Konfiguration

Cluster kann über YAML konfiguriert werden:

```bash
kind create cluster --config myconfig.yaml
```

### Beispiel: Multi-Node-Cluster

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
```

### Beispiel: Ports zum Host weiterleiten

```yaml
extraPortMappings:
  - containerPort: 80
    hostPort: 80
    listenAddress: "0.0.0.0"
```

### Beispiel: Feature Gates aktivieren

```yaml
featureGates:
  SomeFeature: true
```

---

## 🌐 Proxy konfigurieren

Wenn dein Netzwerk einen Proxy erfordert:

```bash
export HTTP_PROXY=http://proxy.example.com
export HTTPS_PROXY=https://proxy.example.com
export NO_PROXY=localhost,127.0.0.1
```

*kind* ergänzt automatisch interne Adressen zu `NO_PROXY`.

---

## 🧾 Logs exportieren

Logs exportieren:

```bash
kind export logs
```

Oder in bestimmtes Verzeichnis:

```bash
kind export logs ./logs
```

Beispielhafte Log-Struktur:

```
.
├── docker-info.txt
└── kind-control-plane/
    ├── containers/
    ├── docker.log
    ├── inspect.json
    ├── journal.log
    ├── kubelet.log
    ├── kubernetes-version.txt
    └── pods/
```
