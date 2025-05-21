o ArgoCD é **pull-based** e **push-based**, isso significa que ele pode tanto aplicar configurações mais atualizadas nos repositórios a que têm acesso.

O componente **Notification Controller** é o componente é responsável por receber notificações dos eventos externos que os repositórios sinalizam, como por exemplo, Hooks configurados para quando o código é sobre uma alteração e para fazer sincronização do estado atual da aplicação com o estado esperado configurado.

## Exposing

Por padrão, o **Notification Controller** utiliza a porta `9292` para receber e notificar, mas para isso, é necessário também expor este controlador para fora do cluster.

### NodePort

Este recurso deve ser apenas utilizado para ambientes de testes para uma pequena equipa, pois, quando sofre bastante carga acaba por ser ineficiente e faz exposição do IP do Cluster.

### Load Balancer

Criar um **Load Balancer** com os recursos nativos do **K8s** é uma alternativa mais esperada para ambientes cooperativos maiores, é a melhor forma de conseguir fazer **HS** (Horizontal Scaling) dos componentes de Notificação.

```yaml
apiVersion: 'v1'
kind: 'Service'
metadata:
	name: 'notification-controller-service-lb'
	namespace: 'namespace'
spec:
	type: 'LoadBalancer'
	selector:
		app: 'notification-controller-app'
	ports:
		- name: 'http'
		  port: 80
		  protocol: TCP
		  targetPort: 9292
```

Apesar de ser mais comum em ambientes corporativos, para produção não é ideal, porque faz exposição do IP do cluster.

### Ingress

A configuração por **Ingress** é a mais utilizada, é possível redirecionar as requisições para um domínio em específico.

```java
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: webhook-receiver
  namespace: flux-system
spec:
  rules:
    - host: flux-webhook.example.com
      http:
        paths:
          - pathType: Prefix
            path: /
            backend:
              service:
                name: webhook-receiver
                port:
                  number: 80
```

É mais eficiente, não faz exposição diretamente do IP do cluster, é mais díficil de configurar.
## Receivers

Os **Receivers** dentro do componente **Notification Controller** são responsáveis por receber as notificações de eventos dos repositórios remotos.

É primeiro necessário criar um Token extremamente seguro, os motivos para isso são para evitar forasteiros de enviar notificações de eventos falsos que poderiam até mesmo apagar a aplicação. Geralmente, a solução mais direta ao se pensar seria talvez deixar o repositório privado. Mesmo isso corrigindo determinados pontos na segurança, outros continuariam por aberto, como por exemplo, se o domínio que utilizamos para recepção de notificações fosse exposto, Então seria na mesma possível enviar requisições falsas.

Para isso é necessário assinar todas as nossas requisições com um **HUB Signature**.

```yaml
apiVersion: 'notification.toolkit.fluxcd.io/v1'
kind: 'Receiver'
metadata:
	name: 'job-info-notification-events-receiver'
	namespace: 'default'
spec:
	type: 'github' # Receivs notifications from github
	events:
		- 'ping'
		- 'push'
	secretRef:
		name: 'job-info-notification-sha-secret'
	resources:
		- kind: 'GitRepository'
		  name: 'job-info-git-repository'
```

E agora a criação do recurso que contém o segredo, em alternativa, pode-se utilizar o **Hashicorp Vault** para poder fazer o gerenciamento dos segredos.

```yaml
apiVersion: 'notification.toolkit.fluxcd.io/v1'
kind: 'Secret'
metadata:
	name: 'job-info-notification-sha-secret'
	namespace: 'default'
type: Opaque
data:
	token: 657ababc3d37508651117aa375053bf67eaed203 # I used SHA algorithm
```

Também é possível fazer o versionamento de imagens do Docker. Existe a possibilidade de criar um **Repository Server** ou utilizar um serviço externo.

Se for para criar um repositório para conter as imagens de forma a que não exista exposição em serviços externos, é possível utilizar o **Harbor**, ferramentas simples, com **Multitencancy** para configuração de equipas, suporta também **Helm Charts** e com chave de ouro ainda possuí uma UI na Web para facilitar toda a gestão de repositórios.

```yaml
apiVersion: 'image.toolkit.fluxcd.io/v1beta1'
kind: 'ImageRepository'
metadata:
  name: 'webapp'
  namespace: 'flux-system'
spec:
  image: 'registry.local:5000/webapp'
  interval: '1m'
  secretRef:
    name: 'regcred' # In case needs to access Docker Registry Service (external)
```




