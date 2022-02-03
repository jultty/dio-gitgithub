*Estas anotações de estudo foram baseadas no conteúdo passado por [Otávio Reis](https://github.com/perkles) no curso **Trabalhando com Branches no GitHub** da Digital Innovation One.*

# Trabalhando com branches

*Criado terça 01 fevereiro 2022*

Branches permitem trabalhar paralelamente em um projeto e mesclar as modificações em um momento futuro (fazer *merge*).

A tag ``HEAD`` representa o estado atual, ou seja, o último commit de uma branch.

Criar uma branch
----------------

O argumento ``checkout`` é usado para movimentar-se entre diferentes branches.

Usando a flag `-b` é possível criar uma nova branch:

```bash
git checkout -b nova-funcionalidade
```

Usando ``checkout`` novamente é possível voltar para a branch principal:

```bash
git checkout main
```

Os arquivos criados no diretório **não ficam** separados entre branches. Assim, ao trocar usando checkout e usar ``git status`` os mesmos arquivos irão aparecer nas duas branches. 

É possível carregar sujeira de uma branch para a outra na forma de arquivos indesejados. Ver adiante no argumento `stash` sobre como evitar isso.

Após fazer um ou mais commits é possível enviar para a nova branch no servidor remoto usando:

```bash
git push origin nova-funcionalidade
```

A nova branch não possui apenas os seus arquivos mas também todos os arquivos da branch principal.

Para juntar as duas branches:

```bash
git checkout main
git merge nova-funcionalidade
```

```
Renomear e apagar
-----------------

Para mudar o nome da branch atual:

```bash
git branch -m novo-nome
```

Para mudar o nome de uma branch qualquer:

```bash
git branch -m nome-atual novo-nome
```

Para apagar uma branch:

```bash
git branch -d nome-da-branch
```

Stash
-----

Entre outras coisas, o argumento `stash` permite guardar nossas alterações e mover entre diferentes branches sem carregar arquivos de uma branch para a outra.

Após editar arquivos e adicioná-los ao staging com ``git add``, usa-se ``git stash save`` para adicionar as modificações à stash na branch atual.

É possível salvar uma descrição com o contexto da stash ao criá-la:

```bash
git stash save "mensagem"
```

E consultar seu conteúdo:

```bash
git stash list
```

Após adicionar os arqivos à stash eles não estarão mais na área de staging:

```bash
git status
# Saída:
# No ramo funcionalidade-grande
# nothing to commit, working tree clean
```

Para abrir a stash e voltar os arquivos para staging:

```bash
git stash pop N
```

Onde ``N`` é o número da stash fornecido pelo comando ``git stash list``.

Finalmente, é possível descartar as alterações na stash com:

```bash
git stash clear
```

Ao fazer isso os arquivos que estavam em **todas** as stashs **serão perdidos**.

git log
-------

Permite visualizar o registro de alterações do repositório, de um diretório ou arquivo:

```bash
git log
git log diret
git log arquivo.java``
```

Usando a flag `--oneline` é possível ver cada commit em uma única linha:

```bash
git log --oneline
```

Para visualizar em forma de gráfico:

```bash
git log --graph
```


