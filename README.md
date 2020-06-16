# Kubernetes

Exemplos demonstrando o uso do kubernetes do básico á cenários mais complexos.
Como ambiente de estudo, utiliza-se o minikube, que pode ser instalado através do link abaixo:
https://kubernetes.io/docs/tasks/tools/install-minikube/

###### Minikube
Subindo um cluster Kubernetes, utilizando o minikube:
```
minikube config set memory 10240
minikube config set cpus 8
minikube config set vm-driver virtualbox
minikube start
```

Configurar o uso do docker dentro do minikube:
```
eval $(minikube docker-env)
```
Retirar o uso do docker dentro do minikube:
```
eval $(minikube docker-env -u)
```
