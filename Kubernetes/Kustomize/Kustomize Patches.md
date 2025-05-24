São formas de tentar criar manifestos com campos mais configuráveis, os campos são incrementais ou alterados sem precisar de criar uma cópia de todo o *kustomize.yaml*, de forma, a que exista uma pequena personalização de campos. É um recurso bastante simples, é eficiente para pequenas alterações.

```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
resources:
	- gotk-components.yaml
	- gotk-sync.yaml
patches:
	- target:
	  group: source.toolkit.fluxcd.io
	  version: v1
	  kind: Kustomization
	  patch: |-
	  - op: replace
	    path: /spec/interval
	    value: ./clusters/dev 
```

