É uma ferramenta plataforma de automação que permite automatizar processos através de **Pipelines** ou projetos **Freestyle**.

* **Master Server** é o servidor principal, que faz a leitura dos repositórios remotos para automação de processos.
  
* **Agents** é uma máquina ou um container que é responsável por executar os steps que configuramos no pipeline. **Permanent Agent** é basicamente uma maquina dedicada para a execução dos passos e os **Cloud Agent** ou **External Agent** é utilizado em um serviço cloud para execução de passos.

Existem várias formas de criar projetos.

* **Freestyle** são projetos simples, são comandos Shell ou Bash. Apenas para configuração de fluxos simples.
  
* **Pipelines**, são arquivos Groovy que são separadas em diversos etapas para execução.
