Vou ser o mais honesto possível, eu tentei dar uma oportunidade ao **Harbor** quando cheguei a parte de instalar **Nexus** com o **Helm**, mas não vale apena, de fato, o **Nexus** consegue ser extremamente melhor que o **Harbor**.

```Bash
helm repo add sonatype https://sonatype.github.io/helm3-charts/
helm install nexus sonatype/nexus-repository-manager --version 64.2.0 --namespace nexus --create-namespace
```

Sim apenas isto, é possível fazer configurações em vários [campos](https://artifacthub.io/packages/helm/sonatype/nexus-repository-manager/28.0.2) mas não acho que vale apena, pelo menos para desenvolvimento e aprendizado, é uma ferramenta incrível. Foi extremamente fácil e demorei poucos segundos para o servidor inteiro inicializar.

Por padrão, ele vêm com um **Service** configurado com **ClusterIP**, o que pode ser mudado por **NodePort** para facilitar ainda mais o uso.