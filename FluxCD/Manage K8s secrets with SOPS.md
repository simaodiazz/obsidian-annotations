O **Sops** ou **Secretive Operations** é uma ferramenta que permite a criptografia segura de recursos que apenas possam ser acessados com o **kustomize-controller** viabilizando práticas de **DevSecOps**.

É possível utilizar vários métodos de criptografia, o mais comum é **age** mas também é possível integrar com o **Hashicorp Vault**.

```sh
age-keygen -o age.agekey # Comando utilizado para gerar uma chave
kubectl create secret generic sops-age --namespace=flux-system --from-file=age.agekey=/dev/stdin
```

Depois disso na raiz do projeto, no `.sops.yaml` é necessário configurar uma propriadade para configurar regras de criação.

```yaml
creation_rules:
  - path_regex: '.*.yaml'
    encrypted_regex: '^(data|stringData)$'
    age: 'AGE_PUBLIC_KEY'
```

E de seguida, é necessário criar uma pasta na raiz do projeto chamada `secrets/` onde vão ser colocados todos os segredos, e de seguida, apenas é necessário guardar o arquivo que ele será automaticamente encriptado.

```Shell
# Este comando 
sops secrets/production.yaml
```

```yaml
apiVersion: v1
kind: Secret
metadata:
	name: app-repository-credentials
	namespace: flux-system
type: Opaque
stringData:
	PASSWORD: clinicadias123
```

## Automatized Integration with Flux

Quando criamos a chave com o comando apresentado anteriormente `age-keygen -o age.agekey`, devemos retirar de lá a chave gerada para colocar aqui.

O arquivo `.sops.yaml` deve continuar a ser criado para definir regras de como produzir recursos criptografados. 

O Flux não faz isso de forma automática, mas é possível utilizar **Git Hooks**, especificamente com o **pre-push** que antes de começar a enviar, conseguir criptografar rapidamente todos os diretórios que contêm secrets.



