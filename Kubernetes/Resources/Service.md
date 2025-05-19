O serviço é um recurso utilizado para expor endereços e portas para fora da rede, existem diversas formas de o fazer nativamente com o Kubernetes, e até com outros recursos fornecidos por outros plugins.

- **NodePort** utilizado para expor uma porta entre 30000 e 32767 e pode ser acessado diretamente com o IPv4 ou IPv6 do serviço.
- **ClusterIP** cria um IP virtual dentro de cluster ou namespace e pode ser utilizado através de um **DNS** e é extremamente eficiente. 