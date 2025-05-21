Arquitetura do **Nexus**, na versão 3 foi implementada e pensada em ser **modular**, **versátil**, **eficiente** para ambientes mais restritos ou com menos recursos.

Ele atua como repositório universal de artefatos, ele consegue ser tão bom, que substitui ferramentas que eram mestres em suas funcionalidades.

* **JFrog Artifactory** que é responsável por versionamento de executáveis de aplicações, geralmente utilizado para guardar versões dos binários executáveis. Em muitos casos, o Nexus consegue desempenhar um papel tão bom como esta ferramenta.

- **Harbor** infelizmente, o que fiz em 6 horas por este ferramenta é uma história, dei tantas oportunidades por ser uma ferramenta extremamente específica, o que geralmente é bom por existir sempre comportamentos esperados de uma ferramenta.

## Núcleo Príncipal

O **Nexus Core** é onde tudo acontece, é onde o **Repository Manager**, responsável pela gestão de todos os repositórios, está alocado. Além de outras funções como.:

* **Database Component** para persistência permanente de informações, se não for configurada, todos os dados irão ser voláteis.

- **Security Component** utilizado para oferecer acesso estilo **RBAC** e **Multitenancy** para criar equipas e utilizadores com determinadas funções.

- **Scheduler** é responsável por executar instruções não imperativas em determinados espaços de tempo

- **Event Bus** é responsável por disparar eventos internos para outros serviços.

## Blob Stores

Todos os artefatos são armazenados em **Blob Stores** que são basicamente utilizados para armazenar **metadados** e o próprio **source code**, existem vários tipos de o fazer, localmente através do **File system** até utilizar o **AS3** (Amazon S3) para armazenamento dos repositórios em um **Cloud Service**.

