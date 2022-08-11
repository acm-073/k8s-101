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
```bash
# im Verzeichnis lab-03
$ kubectl apply -f ingress.yaml -n lab01

# Ingress testen
# external-ip s. oben
curl -H "Host: example.com" <external-ip>/nginx
```

## Zweiter Service
```bash
$ kubectl -n lab01 create deployment web --image=gcr.io/google-samples/hello-app:1.0
$ kubectl -n lab01 expose deployment web --type=ClusterIP --port=8080
```
Ingress Resource modifizieren: Füge zum Ingress eine zweite Path-Regel hinzu (`nano ingress.yaml`):
```yaml
      - path: /web
        pathType: Prefix
        backend:
          service:
            name: web
            port:
              number: 8080
```
Danach muss der Ingress nochmal deployed werden:
```bash
$ kubectl apply -f ingress.yaml -n lab01
# Test des neuen Services
$ curl -H "Host: example.com" <external-ip>/web
```