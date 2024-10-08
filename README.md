# O que é um container?

- Isolamento de recursos

# Container engine

- responsável pela criação do container
- ponto de volume
- Rede
- Não conversa direto com o kernel

# Container Runtime

- Responsável por executar o container
- Conversa direto com o kernel
- high level / low level / sandbox
- container di

# OCI (Open Container Initiative)

consorcio de varias empresas criado para padronizar a criação de containers

desenvolveram o run c

# O que é Kubernetes?

Software responsável por orquestar/gerenciar containers

# Control Plane e Workers

- Control Plane: Responsável por garantir a saúde, disponibilidade, capacidade e armazenar o estado do cluster
- Workers: Máquinas/Nós onde rodam as aplicações

# Componentes do Control Plane

- ETCD: guarda o estado do nosso cluster (como se fosse um banco de chave valor)
- Kube API Server: responsável por conversar com todos os componentes (centralizar)
- Kube Scheduler: Gerenciamento de onde vai rodar os container
- Kube Controller Manager:  gerenciador dos gerenciadores

# Componentes dos Workers

- Kubelet: um serviço executado nos nós que lê os manifestos do container e garante que os containers definidos foram iniciados e estão em execução
- Kube Proxy: Responsável por fazer o container conversar com a internet

# Portas TCP e UDP dos componente do Kubernetes

- Kube-APIServer → 6443 (TCP)
- ETCD → 2379-2380 (TCP)
- Kuber-Scheduler → 10251
- Kubelet → 10250
- Kube-Controller → 10252

Node Port → 30000 - 32767 (TCP)

# Pods, Replicas sets, deployments e service

- Pod: um grupo de um ou mais containers implantados em um único nó. Todos os containers em um determinado pod usam o mesmo endereço IP, IPC, nome do host e outros recursos.
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/c07928da-2fe3-4728-b84b-d40744e3cd60/924386b5-ab7b-4c17-be83-d017c7f68ace/image.png)
    
- Deployment: garante informações, características e recursos as replicas
- Replica set: controller dos pods, garante a quantidade de réplicas
- Service: faz com que os pods sejam acessível de fora do cluster ou do nó

# Instalando Kubectl e Kind

https://kubernetes.io/pt-br/docs/tasks/tools/install-kubectl-linux/

https://kind.sigs.k8s.io/docs/user/quick-start/#installing-from-release-binaries

# Criando nosso primeiro cluster

https://kind.sigs.k8s.io/docs/user/quick-start/

```bash
kind create cluster
```

```bash
kind delete cluster
```

```bash
kind create cluster --config kind-cluster.yml --name giropops
```

OBS: yml

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
```

```bash
kubectl get pods -n kube-system -o wide
```

```bash
kubectl get deployments -A
```

```bash
kubectl get service
```

```bash
kubectl get replicaset
```

# Criando pod

```bash
kubectl run --image nginx --port 80 giropops
```

```bash
kubectl exec -ti giropops -- bash
```

```bash
kubectl delete pods giropops
```

# YAML e kubectl com dry-run

```bash
k run --image nginx --port 80 giropops --dry-run=client
```

```bash
k run --image nginx --port 80 giropops --dry-run=client -o yaml > pod.yaml
```

```bash
k apply -f pod.yaml
```
