Para criar um projeto em Flux, é necessário sempre de muitas coisas.

* Repositório em um **SCM** ou outro **Repository Manager**
* Uma chave **PAT** (**Personal Access Token**) ou uma credencial de acesso.
* E o caminho para onde irão estar todas as configurações do cluster.

Ele vai criar ou usar um repositório já existente e vai criar uma estrutura equivalente a esta.

```Ruby
clusters/
  dev/
    flux-system/
      gotk-components.yaml
      gotk-sync.yaml
      kustomization.yaml
```

É uma estrutura muito simples, **GOTK** significa **GitOps Toolkit**, o arquivo **gotk-components** armazena todos os manifestos que são necessários para a inicialização de todo o próprio **flux-system** e o **gotk-sync** possuí todos os arquivos responsáveis por sincronização com o nosso repositório Github
