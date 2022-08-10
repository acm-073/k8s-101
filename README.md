# k8s-101
Some manifests for a Kubernetes 101 Training

# Set up cluster
Ihr loggt euch mit eurem User auf der Lab-Umgebung ein. Danach könnt ihr mit `minikube` euren persönlichen Kubernetes Cluster aufsetzen.

```bash
$ minikube start --profile $USER
```

**WICHTIG** Wenn ihr den Parameter `--profile $USER` nicht angebt, kommt es zu Namenskonflikten!