O Flux possuí suporte com várias ferramentas que gerenciam ou facilitam a criação de manifestos, mas **Helm** foi recomendada para ser a utilizada.

Eu já usava antes, é extremamente versátil no que se trata a deixar as configurações do nosso Chart mais configuráveis através de **Go Template**.

```yaml
apiVersion: 'source.toolkit.fluxcd.io/v1'
kind: 'HelmRepository'
metadata:
	name: 'podinfo'
	namespace: 'default'
spec:
	interval: '1m' # Update state each 1 minute
	url: 'https://github.com/simaodiazz/github'
```

Caso seja necessário adicionar credênciais para conseguir fazer verificação do código remoto.

```yaml
apiVersion: v1
kind: Secret
metadata:
	name: userInfo
	namespace: default
stringData:
	username: simaodiazz
	password: clínicadias2006
```

Nestes dois manifestos, apenas fazemos com que o Flux use o **Source Controller** para no intervalo de tempo de 1 minuto, faça requests para verificar o estado da aplicação que está a ser executada com o estado que está presente na configuração remota (Github, Bucket, OCI Repository).

```yaml
apiVersion: helm.toolkit.fluxcd.io/v2
kind: HelmRelease
metadata:
  name: podinfo
  namespace: default
spec:
  interval: 10m
  chart:
    spec:
      chart: <name|path>
      version: '4.0.x'
      sourceRef:
        kind: <HelmRepository|GitRepository|Bucket>
        name: podinfo
        url: <url>
        namespace: flux-system
      interval: 10m
  values:
    replicaCount: 2
```

Com este recurso, é possível evitar definir sempre um **Helm Repository**, mas é altamente recomendado definir sempre um, já que é mais organizado e em caso de **Helm Releases** maiores torna-se mais díficil de diferenciar o repositório da própria release.

```yaml
apiVersion: helm.toolkit.fluxcd.io/v2
kind: HelmRelease
metadata:
  name: podinfo
spec:
  chartRef:
    kind: OCIRepository
    name: podinfo
    namespace: flux-system
  interval: 10m
  values:
    replicaCount: 2
```

Esta é a maneira de referenciar diretamente um **Helm Repository** -> **Helm Release**, e na minha modesta observação, é assim que deve ser feito.

Além disso, a outras práticas para definir os valores do Chart, que geralmente acabam por também ser muito grandes, como anteriormente tinha mencionado, ficar díficil de gerenciar o **Helm Release**. É possível utilizar o recurso do kubernetes chamado **ConfigMap** para configuração dos valores do **Helm Release**.

```yaml
apiVersion: helm.toolkit.fluxcd.io/v2
kind: HelmRelease
metadata:
  name: podinfo
spec:
  chartRef:
    kind: OCIRepository
    name: podinfo
    namespace: flux-system
  interval: 10m
  valuesFrom:
	  - kind: ConfigMap
	    name: podinfo-values
```

Se o componente chamado **Notification Controller** for ativado, é possível criar um manifesto com o recurso **Alert** que permite fazer **Logging** de todos os pods.

```yaml
apiVersion: notification.toolkit.fluxcd.io/v1beta3
kind: Alert
metadata:
  name: helm-podinfo
  namespace: flux-system
spec:
  providerRef:
    name: slack
  eventSeverity: info
  eventSources:
  - kind: HelmRepository
    name: podinfo
  - kind: HelmChart
    name: default-podinfo
  - kind: HelmRelease
    name: podinfo
    namespace: default
```
