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
Mecanismo para instalação de recursos dentro do kubernetes e alteração de configuração.
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

###### Ingress
Balanceador de carga, onde as requisições chegarão e serão direcionadas as services.
obs: reuqer um contêiner controlador para estar em execução no cluster.

###### Secrets
Recurso para armazenar e utilizar dados sensíveis, como usuario e senha.
obs: devem ser criptografados em base64.

###### Etcd
É um armazenamento de dados distribuído altamente confiável. Kubernetes usa-o para armazenar todo o estado do cluster. Em um pequeno cluster transitóiro, uma única instância de etcd pode ser executada no mesmo nó com todos os outros componentes mestres. Mas para clusters mais substanticais, é típico ter um cluster de três nós ou até mesmo de cinco nós etcd para redundância e alta disponibilidade.

###### Volumes
É um arquivo ou diretório que pode ser montado em um contêiner em execução em um local especificado pelo usuário.

###### RBAC
Controle de acesso baseado em função, baseia-se em dois conceitos: papel e vinculação. Um papel é um conjunto de permissões sobre recursos definidos como regras. Existem dois tipos de funções: 
- Role, que se aplica a todos os namespaces em um cluste. 
- Binding, está associando uma lista de assuntos com uma função. Existem dois tipos de vinculação: RoleBinding e ClusterRoleBinding, que correspondem a Role e ClusterRole.
Nome do kind: RoleBinging

###### Autoscaling
Mecanismo para escalar nossos pods, conforme o uso de CPU.

### Node components

###### Proxy
Faz limpeza de rede de baixo nível em cada nó.

###### Kubelet
Supervisiona a comunicação com os componentes mestres e gerencia os pods em execução.Exemplo: montagem de volume, executar contêineres no pod e etc.

### Boas práticas

###### Pod banco e dados
Em mecanismos statefull (banco de dados) deve-se fazer uso de um PersistentVolumes, por exemplo o ISCSI (discos baseados em numvem). Outro ponto, crie esses  pods do tipo StatefulSet, onde este mantém uma identidade persistente para cada um.

###### Gerenciamento de certificados
Utilizaremos o cert-manager para provisionar os nossos certificados
```
kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v0.8.1/cert-manager.yaml 
```

### Comandos uteis
- Colocar o ip do minikube dentro do hosts
```
sudo bash -c "echo $(minikube ip) minikube.me | tee -a /etc/hosts"
```
- Apontar para um namespace:
```
kubectl config set-context $(kubectl config current-context) --namespace=spring
```
- Apontar para docker do minikube e gerar a imagem das aplicações
```
eval $(minikube docker-env) ./gradlew build && docker-compose build
```

