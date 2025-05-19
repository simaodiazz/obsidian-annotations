Este recurso é utilizado para definir tipos de armazenamento, ou seja, como o armazenamento funciona declarativamente e funcionalmente.

```yaml
apiVersion: 'storage.k8s.io/v1'
kind: 'StorageClass'
metadata:
	name: {{ .Values.storage.name }}
provisioner: 'kubernetes.io/no-provisioner'
volumeBindingMode: 'WaitForFirstConsumer'
```

*Provisioner* é a opção utilizada para definir como os volumes irão ser providos, quando utilizamos o **no-provisioner**, estamos a declarar que, a alocação deve ser feita de forma manual, esta opção ajuda a evitar alocações de espaço que não seja necessário ou quando um PV alcança o seu limite e tenta alocar outro automaticamente.

*Volume Binding Mode* é a opção que muda a forma de como os volumes são criados, eles podem ser criados imediatamente ou podem ser criados apenas quando realmente necessário.

Além de outras muitas opções que podem ser utilizadas.
