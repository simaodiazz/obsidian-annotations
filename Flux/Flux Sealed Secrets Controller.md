São uma opção alternativa ao **SOPS** mas para armazenamento no **Git**, também utilizados para criptografar **Secrets**. Mas de uma forma mais simples e direta e sem tanta complexidade.

É criado um novo componente no **FluxCD** responsável por criar produzir um **RSA**, ou seja, é criptografia assimétrica, onde é criada uma chave privada e outra pública. 

Para fazer o setup do sealed secrets, é necessário primeiro instalar a ferramenta CLI que pode ser encontrada na página do github do **sealed-secrets**.

De seguida, precisamos de instalar um controlador dentro do **kube-system** ou de outro namespace, apesar de não ser necessário criar outro namespace. Para conter a nossa chave privada que vai ser responsável por descriptografar o nosso **Base64**
