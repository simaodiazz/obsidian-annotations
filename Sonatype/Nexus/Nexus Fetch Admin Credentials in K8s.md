É muito fácil, primeiro temos que descubrir o nome do nosso pod e executar um comando para descubrir o conteúdo da credencial. 

```sh
kubectl get pods -n nexus
kubectl exec -it -n nexus pods/nexus-nexus-repository-manager-65f7d7ddd4-7jbxd -- cat /nexus-data/admin.password
```

Se for muito grande, recomendo a criar um **Pipe** para criar um arquivo automaticamente com todo o conteúdo.
