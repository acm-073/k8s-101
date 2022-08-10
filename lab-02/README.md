# Lab 02

## nginx Deployment als Service verfügbar machen
```bash
# mal über kubectl Bordmittel
# Alternativ könnte man auch eine service.yaml anlegen
$ kubectl expose deploy/nginx-deployment -n lab01 --type=ClusterIP

# Service beschreiben lassen
# 1. erst mal die Pods anschauen.
#    Mit der Option "-o wide" werden die Pod IPs ausgegeben
$ kubectl -n lab01 get pod -o wide

# 2. Service anschauen
#    Beachtet in der YAML-Ausgabe:
#    - ClusterIP des Services
#    - Endpoints, hier stehen genau die Pod IPs drin (s.o.)
#    - Label Selector
$ kubectl -n lab01 get service nginx-deployment

```
## Kleiner Ausflug zu Kubernetes DNS
```bash
# Dieses Kommando startet einen Pod mit einem Container in Kubernetes
# und ermöglicht über eine interaktive Shell, in diesem Container Kommandos auszuführen
$ kubectl run -n lab01 -it --rm client --image=wbitt/network-multitool /bin/sh

# im Container
$ nslookup nginx-deployment
# Output:
#   <service>.<namespace>.svc.cluster.local

# Gibt die nginx Standard Seite aus
$ curl nginx-deployment

# Test-Container beenden
$ exit
```