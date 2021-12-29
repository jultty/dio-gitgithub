# O que é Git?

Git é um sistema de **gerenciamento de versões**, ou seja, sua principal função é guardar as diferentes modificações pelas quais um arquivo passa e permitir que você inspecione e desfaça qualquer mudança.

Ele é usado principalmente no desenvolvimento de software, mas também pode ser usado, por exemplo, se você precisa escrever uma grande quantidade de texto ou gerenciar uma grande quantidade de arquivos e ter certeza de que não perderá seu trabalho conforme eles são alterados.

Outra vantagem do Git é que ele trata-se de um sistema *distribuído*, isto é, não retém seus dados em um único lugar centralizado.

Sendo assim, caso haja um problema na sua máquina ou mesmo no servidor central, se outras pessoas também acompanhavam esse código é possível que elas tenham uma versão atualizada dele, ou ao menos a última versão que obtiveram.

## Como o Git funciona?

### SHA-1
O git usa um algoritmo de criptografia desenvolvido pelo governo dos Estados Unidos chamado SHA-1. O nome vem da sigla "Secure Hash Algorithm 1", que significa "Algoritmo de Hash Segura 1".

"Hash" é a sequência única de letras e números que esse algoritmo retorna para a informação que for processada, permitindo que grandes quantidades de dados sejam comparadas, porque ele sempre retornará a mesma hash para as mesmas informações.

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

O comando acima, "echo", envia as duas frases diferentes - uma com acentuação, e outra sem - para o programa *openssl*, que recebe o argumento sha1 como o algoritmo de encriptação que deverá usar.

Perceba como os resultados dos dois comandos são completamente diferentes, apesar de apenas termos trocado um acento.

Essa sequência de letras e números gerada é chamada de **hash** e ela sempre será a mesma. Se rodarmos agora o mesmo comando com o acento novamente, temos:

```sh
echo "olá, dio" | openssl sha1
(stdin)= 4e6d63bc5dd80b0a6cd0d0890792acb0b892911e
```
Perceba como ele gera o mesmo resultado mais uma vez.

Quando você salva arquivos com o Git, ao invés de comparar caractere por caractere ele obtém a hash do seu arquivo. Enquanto nada for alterado nele, a hash será a mesma. O Git também obtém a hash de um diretório inteiro com múltiplos arquivos. Enquanto essa hash permanecer igual, ele sabe que naquele diretório nada foi alterado.

Você pode testar pessoalmente esses comandos em uma interface de comando de acesso público como algumas das disponibilizadas abaixo:

* [bellard.org](https://bellard.org/jslinux/)
* [linuxcontainers.org](https://linuxcontainers.org/lxd/try-it/)
* [tutorialspoint.com](https://www.tutorialspoint.com/unix_terminal_online.php)

## Instalação

O Git pode ser baixado a partir do site oficial, [git-scm.org](http://git-scm.com/downloads).

Você pode consultar no mesmo site a [documentação oficial](https://git-scm.com/docs/git/pt_BR) também.

## Termos comuns 

* **repositório:**
* **username:**
* **commit/comitar:**
* **remoto:**

## Comandos básicos

Para o uso básico do Git você vai usar os seguintes comandos:

* **git init** Inicializa um repositório git no diretório atual
* **git config --global user.email seu@email.com** configura seu endereço de email
* **git config --global user.name nome** configura seu nome de cadastro
* **git status** Mostra o status atual desse repositório
* **git add nome_do_arquivo** Adiciona o arquivo para ser comitado
* **git add --all** Adiciona todos os arquivos para serem comitados
* **git commit -m "mensagem"** Comita os arquivos preparados anteriormente
* **git remote add origin https://github.com/seu-repositorio.git** Conecta seu repositório local a uma origem remota
* **git pull** Obtém as atualizações do repositório remoto
* **git push origin master** Envia suas alterações locais para o repositório remoto

## Autenticação
Para rodar os comandos acima que envolvem repositórios remotos você terá que se autenticar em algum servidor que ofereça repositórios Git.

Para isso pode ser necessário não só criar uma conta mas também gerar chaves SSH.

- [Veja aqui a documentação do GitHub sobre como gerar e cadastrar chaves SSH](https://docs.github.com/pt/authentication/connecting-to-github-with-ssh)

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
