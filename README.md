# Kubernetes

Exemplos demonstrando o uso do kubernetes do básico á cenários mais complexos (alguns arquivos são baseados aqui https://github.com/brendandburns/kbp-sample).
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

Habilitando o ingress

```
minikube addons enable ingress
```

### Helm
Mecanismo para instalação de recursos dentro do kubernetes.
``` 
curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get-helm-3 > get_helm.sh
chmod 700 get_helm.sh
./get_helm.sh
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

##### Ingress
Balanceador de carga, onde as requisições chegarão e serão direcionadas as services.
obs: reuqer um contêiner controlador para estar em execução no cluster.

###### Secrets
Recurso para armazenar e utilizar dados sensíveis, como usuario e senha.
obs: devem ser criptografados em base64.

###### Volumes
É um arquivo ou diretório que pode ser montado em um contêiner em execução em um local especificado pelo usuário.

###### RBAC
Controle de acesso baseado em função, baseia-se em dois conceitos: papel e vinculação. Um papel é um conjunto de permissões sobre recursos definidos como regras. Existem dois tipos de funções: 
- Role, que se aplica a todos os namespaces em um cluste. 
- Binding, está associando uma lista de assuntos com uma função. Existem dois tipos de vinculação: RoleBinding e ClusterRoleBinding, que correspondem a Role e ClusterRole.

###### Autoscaling
Mecanismo para escalar nossos pods, conforme o uso de CPU.

### Boas práticas

###### Pod banco e dados
Em serviços statefull deve-se fazer uso de um PersistentVolumes, por exemplo o ISCSI (discos baseados em numvem).
