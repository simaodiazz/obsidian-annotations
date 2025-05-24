O **Control-loop** ou **CL** é o componente que fica continuamente a fazer reconciliação continua

Os controladores são bastante modulares, no geral, eles são responsáveis por apenas adicionar novas funcionalidades ao flux-controller.

| Componente                  | Responsável                                        | Descrição                                                            |
| --------------------------- | -------------------------------------------------- | -------------------------------------------------------------------- |
| Source Controller           | Repositórios Git/Helm/OCI                          | Monitora fontes declaradas e atualiza para as versões mais recentes. |
| Kustomization Controller    | Recursos Kustomize e Kubernetes Declarations       | Aplica configurações declarativas no cluster.                        |
| Helm Controller             | Charts Helm                                        | Instala e reconcilia charts Helm com base nos valores declarados     |
| Notification Controller     | Alertas e eventos                                  | Publica notificações para sistemas externos via webhook, Slack, etc. |
| Image Automation Controller | Automação de versionamento de imagens              | Detecta novas imagens e versões para o Git com as imagens novas.     |
| Image Reflection Controller | Detecção de novas tags nas imagens nos registries. | Detecta novas tags nas imagens baseadas nos registries.              |
