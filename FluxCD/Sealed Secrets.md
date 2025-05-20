São uma opção alternativa ao **SOPS** mas para armazenamento no **Git**, também utilizados para criptografar **Secrets**. Mas de uma forma mais simples e direta e sem tanta complexidade.

É criado um novo componente no **FluxCD** responsável por criar produzir um **RSA**, ou seja, é criptografia assimétrica, onde é criada uma chave privada e outra pública. 

É necessário instalar uma aplicação **CLI** chamada **kubesealed** em caso que precisemos de faze-lo de forma imperativa e no o próprio **sealed-controller** que é o componente criado pelo FluxCD utiliza.

Geralmente, é necessário criar um repositório que irá conter todas as credênciais da nossa aplicação.

```yaml
apiVersion: 'helm.toolkit.fluxcd.io/v2'
kind: 'HelmRelease'
metadata:
	name: 'sealed-secrets-git-repository'
	namespace: 'flux-system'
spec:
	chart:
		spec:
			chart: 'sealed-secrets-chart'
			sourceRef:
				kind: 'HelmRepository'
				name: 'sealed-secrets'
			version: '>=0.1.0'
		interval: '1h0m0s'
		releaseName: 'sealed-secrets-release'
		targetNamespace: 'flux-system'
		install:
			crds: 'Create'
		upgrade:
			crds: 'CreateReplace'			
```
