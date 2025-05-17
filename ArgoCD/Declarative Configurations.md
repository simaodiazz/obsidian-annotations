As configurações do ArgoCD podem ser configuradas com os manifestos do Kubernetes ou até mesmo pela **API Server** que na minha opinião é muito mais simples, mas em caso de apenas estar a executar o core, utilizar as configurações apenas também é muito útil.
## Atomic Configurations

As configurações atômicas no ArgoCD são aquelas que apenas podes usar com o nome específico do arquivo, por exemplo `argocd-cm.yaml` só pode ser utilizado para **ConfigMap**

## Multiple Configuration Objects

Depois temos também algumas configurações que devem ter o mesmo nome da aplicação no arquivo, como por exemplo, **Application** e **AppProject**.

## Applications

Todos os campos possíveis para criar um manifesto de [Application](https://argo-cd.readthedocs.io/en/stable/operator-manual/application.yaml)

Além disso, este tópico vai ser visto mais para a frente, mas é possível criar aplicações sobre aplicações com [Cluster Bootstrapping](https://argo-cd.readthedocs.io/en/stable/operator-manual/cluster-bootstrapping/)  

## Projetos

Os projetos são recursos que representam um conjunto de aplicações, ou seja, é possível isolar as aplicações através dos projetos.

Um detalhe importante, geralmente quando é criado um Projeto, ele normalmente é preciso de ser criado fora do namespace do ArgoCD onde toda a extensão é executada para funcionalidades que já descrevi em outros arquivos. Então, se for necessário executar no namespace ArgoCD um projeto, será necessário ter **admin-level access** para conseguir realizar estas alterações.

```yaml
apiVersion: 'argoproj.io/v1alpha1'
kind: 'AppProject'
metadata:
	name: 'project'
	namespace: 'default'
spec:
	description: 'Example of project'
	# Permite a observação de alterações para deploy em todos os repositórios
	sourceRepos:
	- '*'
	# Restringe o deploy das aplicações todas apenas a este namespace ou outros
	destinations:
		- namespace: 'guestbook'
		  server: 'https://kubernetes.default.svc'
	# É possível também restringir criação de recursos
	clusterResourceWhitelist: ...
	namespaceResourceBlacklist: ...
	namespaceResourceWhitelist: ...
	# Criação de toles que iram ser associadas aos utilizadores
	roles:
		- name: 'read-only'
		  description: 'Read-only privilege'
		  policies: ...
		  groups: ...	
```

## Repositories

Os repositórios, sendo eles por exemplo os do **Github** ou do **Gitlabs**, é onde os manifestos do kubernetes para configuração das aplicações iram ser adquiridos.

Existem vários métodos de acesso, não vale apena detalhar todos, mas os dois mais importantes é através de **HTTPS** e via **Github App**.

Geralmente, como os repositórios são privados, é necessário fazer uma configuração Secret para declarar as credênciais de acesso.

```yaml
apiVersion: 'v1'
kind: 'Secret'
metadata:
	name: 'express-repository-secrets'
	labels:
	  # Indicar que é um segredo que vai gerido pelo ArgoCD
	  argocd.argoproj.io/secret-type: 'repository'
spec:
	type: 'git'
	url: 'https://github.com/simaodiazz/express-repository-argo-config'
	username: 'simaodiazz'
	password: 'clinicadp123'
```

### Credênciais

Caso existam múltiplos repositórios em que as credênciais sejam sempre as mesmas, é possível fazer **carry in** das credênciais

```yaml
apiVersion: 'v1'
kind: 'Secret'
metadata:
	name: 'private-repository-for-credentials'
	labels:
		argocd.argoproj.io/secret-type: 'repo-creds'
spec:
	type: 'git'
	url: 'https://github.com/simaodiazz/private-repository-for-credentials'
	username: 'simaodiazz'
	password: 'clinicadp123'
```

Depois nas configurações dos outros Secrets, é necessário fazer os seguintes procedimentos.

```yaml
apiVersion: 'v1'
kind: 'Secret'
metadata:
	name: 'express-repository-secrets'
	labels:
		argocd.argoproj.io/secret-type: 'repository'
spec:
	type: 'git'
	url: 'https://github.com/simaodiazz/express-repository-secrets'
```

## Cluster

Pelo que eu entendi deste recurso, ele basicamente possuí o mesmo comportamento que os repositórios, mas funciona em vários namespaces, não tendo a limitação de apenas funcionar em apenas um namespace.

```yaml
apiVersion: 'v1'
kind: 'Secret'
metadata:
  name: 'mycluster-secret'
  namespace: 'argocd'
  labels:
    argocd.argoproj.io/secret-type: 'cluster'
# Serve para conversão direta do campo config para Base64
type: 'Opaque'
stringData:
  name: 'mycluster.local'
  server: 'https://kubernetes.default.svc'
  # Configuração do cluster para indicar onde as credênciais 'globais' estarão
  config: |
    {
      "bearerToken": "<token-do-service-account>",
      "tlsClientConfig": {
        "insecure": false,
        "caData": "<certificado-base64>"
      }
    }
```
