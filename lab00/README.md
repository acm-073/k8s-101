# Ein erster Blick

# Kubernetes Cluster aufsetzen
Ihr loggt euch mit eurem User auf der Lab-Umgebung ein. Danach könnt ihr mit `minikube` euren persönlichen Kubernetes Cluster aufsetzen.

```bash
$ minikube start --profile $USER
```

**WICHTIG** Wenn ihr den Parameter `--profile $USER` nicht angebt, kommt es zu Namenskonflikten!

## Shell einrichten
```bash
$ echo 'source <(kubectl completion bash)' >>~/.bashrc
$ . ~/.bashrc
```

## Ein erster Blick
```bash
$ kubectl get namespace
$ kubectl get pod -A
$ kubectl get all -A
$ kubectl logs storage-provisioner -n kube-system
$ minikube logs -p $USER
```