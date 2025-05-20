Para automatizar o processo de integração automática aos containers/pods que estão em execução no Container, ou seja, quando existe um atualização no repositório, todas as atualizações devem ser refletidas nesses containers/pods.

**Image Reflector Controller** é o componente responsável por monitorar registries, ou seja, aplicações que armazenam imagens como o **Docker Hub** ou outro **OCI Repository** e refletir *metadados* e *tags* úteis para componentes como **Image Automation Controller** para depois automaticamente atualizar os repositórios do Git.
