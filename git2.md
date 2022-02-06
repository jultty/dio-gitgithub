*Estas anotações de estudo foram baseadas no conteúdo passado por [Otávio Reis](https://github.com/perkles) no curso **Trabalhando com Branches no GitHub** da Digital Innovation One.*

# Trabalhando com branches

*Criado terça 1º de fevereiro de 2022*

Branches permitem trabalhar paralelamente em um projeto e mesclar as modificações em um momento futuro (fazer *merge*).

A tag ``HEAD`` representa o estado atual, ou seja, o último commit de uma branch.

## Criar uma branch

A opção ``checkout`` é usada para movimentar-se entre diferentes branches.

Usando a flag `-b` é possível criar uma nova branch:

```bash
git checkout -b nova-funcionalidade
```

Usando ``checkout`` novamente é possível voltar para a branch principal:

```bash
git checkout main
```

Os arquivos criados no diretório **não ficam** separados entre branches. Assim, ao trocar usando checkout e usar ``git status`` os mesmos arquivos irão aparecer nas duas branches. 

É possível carregar sujeira de uma branch para a outra na forma de arquivos indesejados. Ver adiante na opção `stash` sobre como evitar isso.

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

## Renomear e apagar

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

Entre outras coisas, a opção `stash` permite guardar nossas alterações e mover entre diferentes branches sem carregar arquivos de uma branch para a outra.

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

Visualizar logs
-------

Permite visualizar o registro de alterações do repositório, de um diretório ou arquivo:

```bash
git log
git log diret
git log arquivo.java
```

Usando a flag `--oneline` é possível ver cada commit em uma única linha:

```bash
git log --oneline
```

Para visualizar em forma de gráfico:

```bash
git log --graph
```

## Reverter commits

### git reset

É possível efetuar um reset passando uma hash ou a tag head:

```bash
git reset 49460ff
git reset HEAD
```

Esses comandos têm ainda três variações com as flags `--soft`, `--mixed` e `--hard`.



Para ir diretamente um commit, podemos reverter usando `git reset HASH` onde `HASH` é a hash do commit para o qual estamos revertendo.

Uma segunda forma é orientando-se pela tag `HEAD` usando `git reset HEAD~1`, onde a parte final `~1` significa que a reversão será feita na tag `HEAD` menos uma posição. Alterando este número podemos reverter mais commits em relação a ela:

```bash
# reverte 3 commits em relação a HEAD:
git reset HEAD~3
```

Note que estas operações fazem sentido somente no contexto local. Para reverter arquivos que já foram enviados para o repositório remoto são necessários processos diferentes.

#### Flags do git reset

A flag `--soft` reverte a operação de commit, devolvendo  os arquivos para a staging area. Há uma forma ainda experimental de fazer a mesma operação através do comando `git restore` com a flag `--staged`.

Porque `--mixed` é o valor padrão, ele será utilizado mesmo que não informemos nenhuma flag. Ao contrário de `--soft`, ele não retorna os arquivos para a staging area e sim para o status *untracked*. Para comitá-los será preciso adicionar novamente com `git add`.

Por fim, `--hard` simplesmente **apaga** os arquivos que estavam comitados e portanto deve ser usado com cautela.

### git revert

A diferença entre as duas opções é que ```git revert``` não manipula diretamente os estados dos arquivos mas apenas os commits e por isso não é necessário passar nenhuma flag.

Sua sintaxe é parecida, também usando hashes ou tags para se orientar:

```bash
git revert HEAD~1
```

Ao invés de retirar o último commit, esta opção cria um novo commit revertendo os commits indicados.

## Boas práticas

É interessante evitar misturar a ordem dos commits agrupando-os. Isto significa preferir fazer as modificações relacionadas a uma mesma funcionalidade juntas ou em um único commit e não separadas em vários commits que se intercalam com outros commits de outras funcionalidades, o que dificulta a leitura do registro.

Sobre o uso de inglês ou português nos commits é recomendado observar o contexto da sua empresa ou grupo. O uso de um idioma ou outro pode ser uma barreira a mais em projetos que fazem mais sentido em um contexto local.



Os assuntos de commit devem:

* ser curtos e compreensíveis

* ter até 50 caracteres

* começar com letra maiúscula

* não terminar em ponto

* ser escritos em forma imperativa

* 

Para commits em inglês, seria a forma que vem depois de "*If accepted, this commit will...*" e para commits em português viria após "*se aceito, este commit...*".

O corpo dos commits deve:

* ter os detalhes do commit

* quebrar a linha em 75 caracteres

* identificar sua audiência

* explicar tudo

* usar markdown

* 

Os commits também têm um rodapé que pode ser usado para referenciar assuntos relacionados como um *issue* que estiver atrelado ao commit.



A primeira linha dos commits será registrada como seu título e mostrada para referenciar o commit em alguns pontos das interfaces. Já as demais linhas são também registradas e serão exibidas como o corpo do commit.

## Conceitos avançados

Após adicionar um título e corpo no commit é possível fechar *issues* abertas referenciando-as pelo número:

```git
Closes #5
```

Se for usada a palavra reservada `Ref` é possível amarrar um commit ao outro: 

```git
Ref #123
```

### Commits semânticos

Commits semânticos seguem a lógica de um versionamento semântico, onde em um número como `2.3.6`  o primeiro número (2) representa a versão principal (*major*), definida por modificações que quebram a compatibilidade de uso.

O 3 representa a versão menor (*minor*), reservada para modificações que implementam novas funcionalidades, que podem até ser grandes mas que não afetam a retrocompatibilidade do programa com versões anteriores.

O terceiro número (6) representa a versão de *patch*, que se refere a alterações de dia-a-dia como correções de bugs e outras modificações de baixo impacto.

Mais informações sobre versionamento semântico pode ser encontrado em [semver.org](https://semver.org/) e sobre uma convenção de commits relacionada a versionamento semântico em [conventionalcommits.org](https://www.conventionalcommits.org/en/v1.0.0/).

Este versionamento e o uso de convencões legíveis por máquina permite que as mensagens de commit interajam com outras aplicações.
