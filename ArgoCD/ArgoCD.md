ArgoCD é uma ferramenta **GitOps** que segue um conjunto de regras para um Workflow mais eficiente. Ele consegue fazer deploy automaticamente no cluster do **Kubernetes** baseado no nossa configuração.

Para utilizar o ArgoCD é preciso de criar normalmente dois repositórios.

* **Source code** para manter o código principal, por boas práticas.
* **Configuration** para apenas conter a configuração para o Kubernetes.

O **Git** é a **fonte da verdade** ou seja, toda a configuração do cluster se vai basear no repositório, se alguém tentar fazer alterações manualmente no cluster não vai ser possível porque o ArgoCD automaticamente vai fazer essa alteração.

Para trabalhar com o **ArgoCD** de forma eficiente, é necessário utilizar geralmente uma ferramenta de integração continua, como por exemplo, o Jenkins.

Geralmente, é preciso das seguintes etapas para fazer o ArgoCD funcionar no fluxo correto.:

* Criar uma imagem onde já sejam feitos todos os testes.
* Fazer publicação da imagem por exemplo no **Docker Registry**.
* Depois disso, o código deve ser publicado no **Github**.
* Depois disso, o ArgoCD faz sincronização com o ArgoCD e baseia-se nessa configuração.

O ArgoCD possuí um sistema em caso de falha no cluster inteiro, por exemplo, se eu tiver alocado o meu cluster em um serviço cloud, é possível, configurar ações que façam essa recuperação como a realocação de um novo cluster.

É possível fazer o ArgoCD alcançar o funcionamento de gerenciamento de vários clusters, geralmente, esse mecanismo é utilizado em ambientes distribuidos, onde tenho um cluster em localizações geograficamente diferentes.

Existem várias alternativas para gerenciar multiplos clusters, mas das duas que conheço.:

* Criar uma branch para cada ambiente.
* Criar overlays no Kustomize, que é uma ferramenta nativa do Kubernetes. Similar ao funcionamento do Helm, mas mais simples e integrado nativamente ao Kubernetes.

## Próximos passos

- [Architectural Overview](Architectural%20Overview.md)
- [Core](Core.md)
- [Declarative Configurations](./Declarative%20Configurations.md)
