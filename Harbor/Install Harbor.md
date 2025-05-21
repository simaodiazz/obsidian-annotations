A melhor maneira para instalar o harbor é simplesmente criar um Helm Repository e instala-lo como dependência para facilitar a configuração e evitar criar arquivos de configuração e criar manifestos para ConfigMap na configuração dos manifestos.

```yaml
harbor:
	expose:
		type: nodePort
		tls:
			enabled: false
		nodePort:
			http: 32080
			https: 32443
	  
	harborAdminPassword: "" # vazio indica uso de `existingSecret`
	existingSecretAdminPassword: harbor-admin-password-secret
	
	portal:
		tls:
			enabled: false
	
	nginx:
		tls:
			enabled: false
```

Esta é a maneira que eu configurei o meu **Harbor**, além disso, criei um **secret-sealeds-controller** no meu cluster para conseguir fazer a gestão de segredos de forma mais eficiente, segura e compartilhável.
