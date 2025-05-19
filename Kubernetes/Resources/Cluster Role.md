É utilizado para definir um conjunto de políticas que podem ser aplicadas globalmente em todo o cluster ou apenas em determinados namespaces específicados.

```yaml
apiVersion: 'rbac.authorization.k8s.io/v1'
kind: 'ClusterRole'
metadata:
	name: {{ .Values.namespace.name }}-admin
rules:
	- apiGroups: ["*"]
	  resources: ["*"]
	  verbs: ["*"]
```

Aqui eu estou a criar uma role que está exposta a nível de cluster e que pode ser associada a qualquer **ServiceAccount** através de **ClusterRoleBinding**.
