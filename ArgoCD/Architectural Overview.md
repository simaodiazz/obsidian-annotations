## API Server

É responsável por fornecer uma UI para a gestão das nossas aplicações no ArgoCD, além de outras operações como de **Rollback** e **Sincronização**, sendo possível também fazer a gestão de utilizadores e de cargos **RBAC**. 

Este servidor suporta dois protocolos de comunicação, o **gRPC** por ser rápido e eficiente em comunicações internas e **REST** para padronização de comunicação na web. 

O motivo pelo uso de **gRPC** em determinadas camadas internas do **ArgoCD** é justamente por sua eficiência na codificação com **Protobuf**, que é feita em binário, reduzindo o tamanho das mensagens quase exponencialmente, e o uso de **REST** é justamente por ser mais padronizado e a maioria das linguagens consegue interpretar mensagens JSON justamente por ser um padrão altamente conhecido, ao contrário do **gRPC**, que é suportado por pouco mais de 11 linguagens.

Um exemplo mais básico, é que o gRPC é utilizado por exemplo no **CLI** enquanto o **REST** é utilizado acessando o site por exemplo ou fazendo uma requisição ao próprio serviço **kubernetes.default.service**.

## Repository Server

É um serviço responsável por manter uma cópia do repositório remoto em cache local, ele faz a gestão de todos os manifestos, ou seja, configurações que fizemos com ferramentas como **Kustomize** ou **Helm**.

O ArgoCD possuí plugins internos para a renderização dos manifestos, já que como disse anteriormente, eles podem ser manifestos criados a partir do **Helm** ou do **Kustomize** ou até mesmo **Plain Yaml**, esses plugins chamam-se **Template Render Plugins**.

- Continuar a partir de (http://argo-cd.readthedocs.io/en/stable/operator-manual/architecture/)




