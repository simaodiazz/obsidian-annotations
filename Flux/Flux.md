O **FluxCD** é uma ferramenta parecida ao **ArgoCD**, só que é mais usada em ambientes onde a declaratividade de configurações é necessária. Não possuí uma **UI** como o ArgoCD fornece a **API Server** para criar aplicações e fazer a gestão delas. Então, acaba por ser mais simples, depende fortemente de um **CI** para automatização completa, ao contrário do **ArgoCD** que sempre necessita de mão humana.

Em uma observação geral, o FluxCD possuí menos **Footprint** e **Overhead** de execução, eu pelo menos, prefiro o FluxCD juntamente com outras ferramentas que o usam para visualização gráfica, é mais eficiente do que possuir um **API Server** com **UI integrada**.

Uma boa observação do **FluxCD** é que ele é que a configuração de novos utilizadores é extremamente simples, posso utilizar os próprios **ServiceAccount** do Kubernetes para criar novos utilizadores, isso facilita tudo, além, de padronizar a forma como os utilizadores são criados.

Permite também **Multitenancy** que é a capacidade de criar equipas ou grupos de utilizadores que possam gerenciar de forma isolada os recursos associados a eles.

O ArgoCD é mais imperativo em relação ao FluxCD, ele tenta ser mais declarativo, ou seja, ele tenta evitar receber ordens diretas e sim apenas executar aquelas que já foram configuradas de forma declarativa.

Na minha observação geral, o ArgoCD é uma ferramenta boa para iniciantes e gestão em uma empresa pequena a média escala, o FluxCD é mais específico para este proposito de automatização.

# Próximos Passos

* [Flux Simple Commands](Flux%20Simple%20Commands.md)
* [Flux Ways to structure your repositories](Flux%20Ways%20to%20structure%20your%20repositories.md)
* [Flux Manage Helm Releases](Flux%20Manage%20Helm%20Releases.md)
* [Flux Setup Webhook Receivers](Flux%20Setup%20Webhook%20Receivers.md)
* [Flux Manage K8s secrets with SOPS](Flux%20Manage%20K8s%20secrets%20with%20SOPS.md)
* [Install SOPS](Install%20SOPS.md)
* [Flux Sealed Secrets Controller](Flux%20Sealed%20Secrets%20Controller.md)
* [Flux Difference beetwen use SOPS and Sealed Secrets](Flux%20Difference%20beetwen%20use%20SOPS%20and%20Sealed%20Secrets.md)
* [Flux Automate image updates to Git](Flux%20Automate%20image%20updates%20to%20Git.md)





