### Avaliação - Arquitetura e Administração de Containers, Microservices, Kubernetes


## QUESTÃO 01 - DOCKER

### 1.Clone o projeto:

```bash
git clone https://github.com/evandrocustodio/springboot-backend-avaliacao.git
```

### 2.Edite o arquivo src/main/resources/application.properties 
e altere o valor da propriedade aluno.nome para o seu nome 
completo;

### 3.Gere a imagem:

rodar o comando abaixo no caminho ..\avaliation\questao1\springboot-backend-avaliacao

```bash
docker build -t migueljefferson/avaliacao:backend .
```

### 4.Faça o push da imagem gerada para o seu repositório 
dockerhub.

```bash
docker push migueljefferson/avaliacao:backend
```

### 5.Gere uma tag da imagem criada para:

```bash
docker build -t migueljefferson/avaliacao:backend-tag .
```

### 6.Faça o push da tag gerada para o seu repositório 
dockerhub.

```bash
docker push migueljefferson/avaliacao:backend-tag
```

### 7.Deixe as imagens públicas.

https://hub.docker.com/repository/docker/migueljefferson/avaliacao/general


## QUESTÃO 02 - DOCKER

### 1.Clone o projeto:

https://github.com/evandrocustodio/react-frontend-avaliacao

```bash
git clone https://github.com/evandrocustodio/react-frontend-avaliacao.git
```

### 2.Gere a imagem:

```bash
docker build -t migueljefferson/avaliacao:frontend .
```

### 3.Faça o push da imagem gerada para o seu repositório 
dockerhub.

```bash
docker push migueljefferson/avaliacao:frontend
```

### 4.Gere uma tag da imagem criada para:

```bash
docker build -t migueljefferson/avaliacao:frontend-tag .
```

### 5.Faça o push da tag gerada para o seu repositório 
dockerhub.

```bash
docker push migueljefferson/avaliacao:frontend-tag
```

### 6.Deixe as imagens públicas.

https://hub.docker.com/repository/docker/migueljefferson/avaliacao/general


## QUESTÃO 03 - DOCKER
### 1.Instancie os containers:
### Observações: trocar o nome

```bash
docker run -d --rm --name postgres -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=avaliacao -e POSTGRES_DB=avaliacao -e POSTGRES_HOST_AUTH_METHOD=trust postgres:15.2
```

```bash
docker run -d --rm --name backend --link postgres:postgres -e DB_HOST_NAME=postgres -e DB_PORT=5432 -e DB_NAME=avaliacao -e DB_PASSWORD=avaliacao -p 8080:8080 migueljefferson/avaliacao:backend
```

```bash
docker run -d --rm --name frontend --link backend:backend -p 3000:80 migueljefferson/avaliacao:frontend
```

### 2. Print a tela com o resultado do comando: 

```bash
docker ps -a
```

### 1. Acesse o backend e capture a tela dos seguintes serviços:
- http://localhost:8080/info
- http://localhost:8080/despesas/

4.Acesse o frontend e capture a tela:
- http://localhost:3000/


## QUESTÃO 04 – DOCKER-COMPOSE e DOCKER SWARM

### 1.Construa um serviço na versão 3 para os 3 containers da questão 03.

- arquivo criado
docker-compose.yml

#### Iniciar swarm

```bash
docker swarm init
```

#### Instânciar serviço

```bash
docker stack deploy -c docker-compose.yml avaliacao
```

#### Remover serviço

```bash
docker stack rm avaliacao
```

## QUESTÃO 05 – KUBERNETES - PODS

Abra o arquivo App.tsx e altere a linha 15 e gere novamente a
imagem do frontend. (arquivo já corrigido)

#### Criar imagem frontend
```bash
docker build -t migueljefferson/avaliacao:frontend .
```

#### Criar pods postgres
```bash
kubectl apply -f postgres-pod.yml
```
#### Ver IP pod
```bash
kubectl describe pods
```
Obs.: alterar o ip do arquivo backend-pod.yml com o ip do postgres

#### Criar pods backend e frontend

```bash
kubectl apply -f backend-pod.yml
kubectl apply -f frontend-pod.yml
```

#### Remover Pod individual
```bash
kubectl delete -f backend-pod.yaml
```

### 1.Crie os arquivos YAML para a criação dos PODS para os 3 containers da questão 3.

### 2.Lembre de colocar as tags:
app: postgres, app: backend e app: frontend nos respectivos PODS.

### 3.Instancie os 3 PODS

### 4.Capture a tela com o resultado do comando: 

```bash
kubectl get pods
```
### 5.Remova os 3 pods. 

#### Remover todos os Pods
```bash
kubectl delete pods --all
```

## QUESTÃO 06 – KUBERNETES - DEPLOYMENTS
1.Crie os arquivos YAML para a criação dos DEPLOYMENTS para os 3 containers da questão 3.

#### Criar pods postgres
```bash
kubectl apply -f postgres-deploy.yml
```
#### Ver IP pod
```bash
kubectl describe pods
```
- Obs.: alterar o ip do arquivo backend-deploy.yml com o ip do postgres

#### Criar pods backend e frontend

```bash
kubectl apply -f backend-deploy.yml
kubectl apply -f frontend-deploy.yml
```

### 2.Lembre de definir 3 instâncias para o FRONTEND

### 3.Instancie os 3 DEPLOYMENTS

### 4.Capture a tela com o resultado do comando:
```bash 
kubectl get all
```