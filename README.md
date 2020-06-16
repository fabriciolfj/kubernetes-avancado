# Kubernetes

Exemplos demonstrando o uso do kubernetes do básico á cenários mais complexos.
Como ambiente de estudo, utiliza-se o minikube, que pode ser instalado através do link abaixo:
https://kubernetes.io/docs/tasks/tools/install-minikube/

### Minikube
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

### Conceitos

###### Deployment
É a implantação dos nosso recursos, e nesta api que definimos as cotas, quantidades de réplicas, qual imagem utilizar para nosso pod (menor unidade dentro do kubernetes, aonde são executado o microserviço) e mapeamento de volumes.

###### Service
Mecanismo onde vou êxpor minha implantação, para ser acessada por outros sistemas, sejam esses implantados dentro do cluster do kubernetes ou externos.

###### Namespace
Isolar diferentes partes do seu cluster um do outro. Pods em execução em um namespace so podem acessar diretamente seu próprio namespace. Para acessar outros namespaces, eles devem passar por APIs públicas.

###### Service accounts
As contas de serviço fornecerem identidade aos seus microserviços. Cada conta de serviço terá certos privilégios e direitos de acesso associados à sua conta.

###### Secrets
Recurso para armazenar e utilizar dados sensíveis, como usuario e senha.
obs: devem ser criptografados em base64.