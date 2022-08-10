# Lab 03

**Hinweis** Ihr braucht hierfür zwei Terminals mit SSH-Verbindung zur Lab-Umgebung.

## Ingress Deployment
Geht in minikube ganz einfach...
```bash
$ minikube addons enable ingress -p $USER
$ kubectl -n ingress-nginx patch service ingress-nginx-controller -p '{"spec":{"type":"LoadBalancer"}}'
```
## Ingress zugreifbar machen
```bash
# WICHTIG: in einem zweiten Terminal ausführen!
# Dieses Kommando kehrt nicht zurück, so lange der Tunnel läuft.
$ minikube tunnel -p $USER
```

## Auf Ingress zugreifen
```bash
# Ingress Service abrufen, beachte das Feld EXTERNAL-IP
$ kubectl get svc ingress-nginx-controller -n ingress-nginx

# Ingress aufrufen
$ curl <external-ip>
# ... sollte eine 404 Not Found Seite zurückgeben
```

## Ingress Resource deployen