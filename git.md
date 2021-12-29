# O que é Git?

Git é um sistema de **gerenciamento de versões**. Sua principal função é guardar as diferentes modificações pelas quais um arquivo passa e permitir que você inspecione e desfaça qualquer alteração.

Ele é usado principalmente no desenvolvimento de software, mas também pode ser usado, por exemplo, se você precisa escrever uma grande quantidade de texto ou gerenciar muitos arquivos e ter certeza de que não perderá seu trabalho conforme eles são alterados.

Estudantes, por exemplo, utilizam o Git ao escreverem trabalhos de conclusão de curso, porque assim sabem que não perderão seus arquivos e que poderão voltar atrás caso desejado.

Outra vantagem do Git é que ele trata-se de um sistema *distribuído*, isto é, não guarda seus dados em um único lugar.

Sendo assim, caso haja um problema na sua máquina ou mesmo no servidor, se outras pessoas também acompanhavam esse código é possível que elas tenham uma versão atualizada dele, ou ao menos a última versão que obtiveram.

## Como o Git funciona?

### SHA-1

O git usa um algoritmo de criptografia desenvolvido pelo governo dos Estados Unidos chamado SHA-1. O nome vem da sigla "Secure Hash Algorithm 1", que significa "Algoritmo de Hash Segura 1".

Na programação, uma *função* é um código que pode ser executado repetidamente no mesmo programa, recebendo diferentes informações de entrada a cada vez que é executado e dando um retorno de acordo com elas. Um tipo de função é a *função hash*.

A função hash do algoritmo SHA-1 gera uma sequência única de letras e números que sempre é a mesma para a mesma informação processada, permitindo que grandes quantidades de dados sejam comparadas, porque este retorno será sempre o mesmo contanto que as informações recebidas sejam as mesmas.

Veja aqui dois exemplos de hashs:

* 4e6d63bc5dd80b0a6cd0d0890792acb0b892911e
* 313a108390fa72d3cd006eef91081c3247a98fbc

Apesar de longas e cheias de caracteres, essas duas hashs são o resultado da simples frase "olá, dio" quando passada pelo algoritmo SHA-1. E apesar de serem completamente diferentes, elas foram geradas apenas colocando ou não o acento agudo em "olá".

Esses foram os comandos usados para gerar cada hash:

```sh
echo "olá, dio" | openssl sha1
(stdin)= 4e6d63bc5dd80b0a6cd0d0890792acb0b892911e

echo "ola, dio" | openssl sha1
(stdin)= 313a108390fa72d3cd006eef91081c3247a98fbc
```

O comando acima, "echo", envia as duas frases diferentes - uma com acentuação, e outra sem - para a saída do terminal. O caractere "|" passa essa saída para o programa *openssl*, que recebe o argumento **sha1** como o algoritmo de encriptação que deverá usar.

Perceba como os resultados dos dois comandos são completamente diferentes, apesar de apenas termos trocado um acento.

Formalmente, *hash* é o nome da função que gera essa sequência de letras e números, mas é comum ver a própria sequência também sendo chamada de *hash*.

Essa sequência sempre será igual para uma mesma entrada. Se rodarmos agora o mesmo comando com o acento novamente, temos:

```sh
echo "olá, dio" | openssl sha1
(stdin)= 4e6d63bc5dd80b0a6cd0d0890792acb0b892911e
```

A saída é o mesmo resultado, 4e6d...

Quando você salva arquivos com o Git, ao invés de comparar o conteúdo em caracteres ele obtém a hash do seu arquivo. Enquanto nada for alterado nele, a hash será a mesma. O Git também obtém a hash de um diretório inteiro com múltiplos arquivos. Enquanto essa hash permanecer igual, ele sabe que naquele diretório nada foi alterado.

Você pode testar pessoalmente esses comandos em uma interface de comando de acesso público como algumas das disponibilizadas abaixo:

* [bellard.org](https://bellard.org/jslinux/)
* [linuxcontainers.org](https://linuxcontainers.org/lxd/try-it/)
* [tutorialspoint.com](https://www.tutorialspoint.com/unix_terminal_online.php)

## Instalação

O Git pode ser baixado a partir do site oficial, [git-scm.org](http://git-scm.com/downloads).

No mesmo site você pode consultar também a [documentação oficial](https://git-scm.com/docs/git/pt_BR) em português.

## Termos comuns

* **repositório:** Um diretório (pasta) de arquivos cujos conteúdos estão sendo acompanhados com o git
* **username:** O nome guardado na variável *user.name* que será usado para autenticar-se em um servidor remoto. Deve ser o mesmo cadastrado no servidor.
* **commit/comitar:** Antes de enviar suas mudanças, o Git pede que você *comite* elas. Commit quer dizer literalmente *comprometer*, ou seja, ao comitar você atesta que foi você quem fez as mudanças e informa uma mensagem explicando o que foi feito. O commit contém as informações de quem, quando e o que foi alterado. O registro de versões do Git consiste numa sequência dos commits que cada pessoa envia para o repositório.

## Comandos básicos

Para o uso básico do Git você vai usar os seguintes comandos:

| Comando                                                          | Descrição                                              |
|:---------------------------------------------------------------- |:------------------------------------------------------ |
| **git init**                                                     | Inicializa um repositório git no diretório atual       |
| **git config --global user.email seu@email.com**                 | configura seu endereço de email                        |
| **git config --global user.name nome**                           | configura seu nome de cadastro                         |
| **git status**                                                   | Mostra o status atual desse repositório                |
| **git add nome_do_arquivo**                                      | Adiciona o arquivo para ser comitado                   |
| **git add --all**                                                | Adiciona todos os arquivos para serem comitados        |
| **git commit -m "mensagem"**                                     | Comita os arquivos preparados anteriormente            |
| **git remote add origin https://github.com/seu-repositorio.git** | Conecta seu repositório local a uma origem remota      |
| **git pull**                                                     | Obtém as atualizações do repositório remoto            |
| **git push origin master**                                       | Envia suas alterações locais para o repositório remoto |

## Autenticação

Para rodar os comandos acima que envolvem repositórios remotos você terá que se autenticar em algum servidor que ofereça repositórios Git.

Dependendo do serviço que você utilizar, pode ser necessário não só criar uma conta mas também gerar chaves de autenticação.

- [Veja aqui a documentação do GitHub sobre como gerar e cadastrar chaves com SSH](https://docs.github.com/pt/authentication/connecting-to-github-with-ssh)

## Outras plataformas

Além do GitHub existem outras plataformas de Git que você também pode utilizar se preferir:

- [GitLab](https://gitlab.com/explore/projects/trending)
- [Codeberg](https://codeberg.org/)
- [sourcehut](https://sourcehut.org/)
- [Bitbucket](https://bitbucket.org/)

E você também pode hospedar um software que gerencia repositórios Git no seu próprio servidor se você tiver um:

- [Gitea](https://gitea.com)
- [Gogs](https://gogs.io/)
- [Self-managed GitLab](https://about.gitlab.com/install/)
