Existem diversas formas para estruturar o nosso repositório que irá conter todos os manifestos para os nossos clusters que o FluxCD irá utilizar. 

Umas estruturas oferecem mais flexíbilidade, geralmente essas estruturas usam **HelmReleases** para versionamento fácil de aplicações, e as mais simples e diretas que apenas utilizam **Kustomize** para quem não gosta de trabalhar com **Go Template**

## Monorepositório

```console
├── apps
│   ├── base
│   ├── production 
│   └── staging
├── infrastructure
│   ├── base
│   ├── production 
│   └── staging
└── clusters
    ├── production
    └── staging
```

Esta é uma estrutura para projetos bastante modestos, a pasta de aplicações é onde ficam as nossas aplicações, como servidores próprios. Na pasta de infrastrutura ficam aplicações que utilizamos geralmente para **GitOps** ou **GitSecOps** (versão atualizada do GitOps mas com seguran aprimorada) e na pasta clusters ficam diretamente os arquivos que ajudam o FluxCD a fazer o Diçaff do estado com o atual, é onde normalmente ficam os manifestos que referênciam os nossos repositórios.

## TBD

**Trunck-based Development** define uma metodologia de desenvolvimento onde a **main** é a branch do projeto mais atualizada, e vão sendo criados **PRs** em branches diferentes e com suante fossem sendo juntados a branch **main** iriam sendo apagadas em consequência.

O Mono repositório hoje é basicamente utilizado como base para todos os outros, apenas mudando a complexidade e a diversidade de pastas para organização arquitetural. Então por exemplo estruturas como **Organization Repository** ou **Team Repository** apenas seriam extensões deste padrão, não vou perder tempo a escrever sobre estruturas cujos os nomes são legíveis e facilmente entendíveis.

## Flagger

Um extra, em aplicações grandes, geralmente com muitos testes. Podem sempre acontecer problemas mesmo quando todos os testes configurados não alertam problemas.

Existe uma técnica chamada Flagger, em que todo o tráfico vai sendo levemente direcionado para o ambiente de produção, como se fosse uma torneira, geralmente não se pode puxar de repente, porque se não a água vêm forte de mais e vai respingar no fundo, então têm que se ir abrindo devagar. 

Também existem uma extensões deste padrão, geralmente é o que nunca falta, na minha observação, são coisas fáceis de pensar. Então ter apenas isto em mente de forma a que se possa desenvolver mais ideias baseadas nisto de forma rápida no futuro.
