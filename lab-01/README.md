# Lab 01
## Namespace
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

## Deployment
```bash
$ kubectl apply -f deployment.yaml -n lab01

# Check pods
$ kubectl get pod -n lab01
```
## Was passiert ist
Führt diese Befehle evtl. ein paar mal hintereinander aus, um zu sehen wie die "Reconciliation" abläuft.
```bash
$ kubectl get event -n lab01

# observe the "status" section
$ kubectl get deployment nginx-deployment -n lab01
```

```bash
# Get logs from pod
# should be empty on first attempt
$ kubectl logs nginx-deployment-xxxxxxx-yyyy -n lab01

# Access port of one pod
# Use your assigned port (see MIRO board)
$ kubectl port-forward nginx-deployment-xxxxxxx-yyyy -n lab01 <yourport>:80
```
Jetzt könnt ihr ein zweites Terminal starten und dem nginx über den weitergeleiteten Port eine Anfrage schicken:
```bash
$ curl localhost:<yourport>
```
Es sollte ein HTML-Dokument ausgegeben werden mit dem Inhalt "Welcome to nginx! [...]"

Wenn ihr jetzt nochmal die Logs abruft (s.o.), dann sollte im Log eine Access Log-Zeile stehen.

## Was sonst noch so geht
```bash
# Deployment skalieren
$ kubectl -n lab01 scale deploy/nginx-deployment --replicas 2

# Logs des ganzen Deployments
# über Label Selector
$ kubectl logs -n lab01 -l app=nginx

# Neue Container-Version
$ kubectl patch deployment nginx-deployment -n lab01 -p \
  '{"spec":{"template":{"spec":{"containers":[{"name":"nginx","image":"nginx:1.23.1"}]}}}}'
```