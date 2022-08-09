# Lab01
## Create Namespace
```bash
# Check existing namespaces:
$ kubectl get namespace

# Create Namespace for lab
$ kubectl create namespace lab01
```
**Pro Tip**
Wer nicht jedesmal bei kubectl den Namespace mit `-n lab01` angeben will, setzt im Kontext den Default Namespace:
```bash
# Modify context to use new namespace by default
$ kubectl config set-context --current --namespace=lab01
```

## Create deployment
```bash
$ kubectl apply -f deployment.yaml -n lab01

# Check pods
$ kubectl get pod -n lab01

# Get logs from pod
# should be empty on first attempt
$ kubectl logs nginx-deployment-xxxxxxx-yyyy -n lab01

# Access port of one pod
# choose a random port above 10000
$ kubectl port-forward nginx-deployment-xxxxxxx-yyyy -n lab01 <random>:80
```
Jetzt könnt ihr ein zweites Terminal starten und dem nginx über den weitergeleiteten Port eine Anfrage schicken:
```bash
$ curl localhost:<random-port>
```
Es sollte ein HTML-Dokument ausgegeben werden mit dem Inhalt "Welcome to nginx! [...]
