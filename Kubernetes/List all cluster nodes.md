```Shell
kubectl get nodes -o wide
```

Este comando é responsável por adquirir todos os nodes do teu cluster, sendo eles do propósito **control-panel** ou **worker-node**

a opção `-o` é utilizado para fazer modificações no output, como é visível, eu estou a acrescentar uma opção chamada `wide` para adicionar mais informações ao output do comando.
