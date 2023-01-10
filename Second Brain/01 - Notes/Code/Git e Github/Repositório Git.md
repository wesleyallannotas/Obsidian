---
title: Entenda sobre repositório git
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [git]
description: Como controlar nosso repositório git
---
# Criando Repositório
Para iniciarmos o versionamento do nosso projeto, basta rodas o seguinte comando.

```bash
git init
```

Criando o diretório oculto `.git` que armazena as configurações e o versionamento do projeto.

# Clonando um Repositório
Podemos clonar um repositório do Github facilmente de diferentes modos, seja via `http` ou `ssh`, através do seguintes comandos

```bash
git clone https://github.com/nomeUsario/nomeRepo.git  // HTTP
git clone git@github.com:nomeUsario/nomeRepo.git  // SSH
```

Será clonado todo o repositório para a maquina local, trazendo todos os _commits_ e tudo mais.

# Adicionando Modificações
Após realizarmos alterações de qualquer natura no nosso repositório Git, essas modificações ficaram em estado de _modified_, onde mesmo que realizarmos um _commit_ essas alterações não entraram, pois, é necessário adicionar as modificações na _Stage Area_, essa estrutura possibilita selecionarmos arquivos para o _commit_, invés de levar todos, adicionamos os arquivos ao estado de _Staged_ através do comando

```bash
git add <arquivo>
git *.md
git add .
```

Quando utilizamos o `.` é adicionada todas as modificações de uma vez, ou seja, todas os arquivos em estado de _modified_ é levado para _Staged_

## Revertendo de _Staged_
Após alterar o status da modificação para _Staged_, ou seja, adicionar os arquivos alterador a _Stage Area_, pode nos ocorrer de se arrepender, querer que essa alteração vá apenas no próximo _commit_, ou qualquer outro motivo, desta forma podemos usar o seguinte comando.

```bash
git restore --staged <arquivo>
```

Assim o arquivo volta para o _Working Diretory_, mantendo as alterações.

>[!note] Outro forma
>Podemos remover um arquivo da _Stage Area_ de outra forma também, uma forma mais antiga, basicamente é utilizando o comando
>```bash
>git reset HEAD arquivo
>```
>Lembrando que o [[Introdução ao Git#Ponteiro HEAD|ponteiro HEAD]], por padrão aponta para o ultimo _commit_, porem podemos manipular.

# Revertendo Alterações
Após realizar a modificação de um arquivo, podemos nos ocorrer de querer reverter essa alteração, independente de qual seja, o Git nos permite, porem os arquivos devem se encontrar no _Working Diretory_, ou seja, caso se encontrem na _Stage Area_, é necessário [[#Revertendo de _Staged_|reverter]], assim podendo realizar o comando

```bash
git restore <arquivo>
```

# Removendo Arquivo via Git
Podemos remover um arquivo do nosso diretório Git, diretamente através do seguinte comando.

```bash
git rm <arquivo>
```

Desta forma o arquivo é removido e sua modificação deleção vai direto para _Stage Area_, o `rm` do Git tem o mesmo funcionamento do `rm` dos sistemas de base Unix, ou seja, é deletado totalmente do sistema, ou seja, não tem recuperação.

# Movendo e Renomeando via Git
Podemos mover ou remover arquivos diretamente pelos comandos Git através do seguinte comando.

```bash
git mv ./path/arq ./newPath/arq
git mv arq newNameArq
```

Podemos perceber que seu funcionamento é o mesmo do `mv` dos sistemas de base Unix, ou seja, podemos utilizar o comando para renomear e mover arquivos.

# Removendo Arquivos Não Rastreados
Podemos remover arquivos não rastreados, ou seja, arquivos que nunca fizeram parte do nosso repositório através de um simples comando, teve se tomar cuidado, pois, não tem volta, o arquivo não vai para lixeira.

```bash
git clean -n
```

# Criando Commit
Com as alterações desejadas adicionadas a _Stage Area_ podemos registrar o _commit_, através do comando.

```bash
git commit -m "init"
```

Com a _flag_ `-m` adicionamos uma mensagem ao nosso _commit_, normalmente uma mensagem curta que identifica as alterações realizadas.

# Corrigindo Commit
Temos que lembrar que um _commit_ esta relacionado um com o outro, criando uma espécie de apontamentos como ocorre na _linked list_ ou em português lista encadeada, o que traz uma certa complexidade para  alterações em _commits_ muito antigos, necessitando uma maior conhecimento, porem no nosso ultimo _commit_ é algo mais tranquilo de se alterar, assim podendo ser alterado das seguintes formas, obviamente será gerado uma nova _hash_ é gerada, pois, é [[Introdução ao Git#Nome dos Commits|gerada]] partir das informações do _commit_.

```bash
git commit --amend -m "Alerando Mensagem"
```

Para alterar os arquivos junto, basta adiciona-los a _Stage Area_, que realizando esse comando ele vai para o _commit_ anterior, caso não especifica uma nova mensagem será perguntando se deseja manter a mesma.

# Buscando Alterações Antigas
Podemos recuperar arquivos de _commit_ anteriores caso haja a necessidade, será necessário o inicio do [[Introdução ao Git#Nome dos Commits|nome do commit]] que é a _hash_ exibida quando usamos o comando `git show`, e que seja escrito da seguinte forma

```bash
git checkout edcdf19 -- arquivo
```

`edcf19` é um exemplo de inicio de _hash_, podemos pegar esse inicio da _hash_ através do comando `git log --oneline`

# Revertendo Commits
Podemos reverter a um _commit_ antigo facilmente, através do seguinte comando

```bash
git revert HEAD~5
```

Sabemos _HEAD_ simboliza o [[Introdução ao Git#Ponteiro HEAD|ponteiro]] do nosso diretório, onde por padrão caso não manipulado manualmente, aponta para o ultimo _commit_, nesse caso estamos revertendo para 5 _commits_ antes do ponteiro, como o Git não acha interessante apagar _commits_, na realidade será criado um novo _commit_ trazendo as informações desse _commit_ anterior, será necessário dar um nome para esse _commit_ após executar o comando.
Também é possível utilizar uma parte da _hash_ que é obtida através de `git log --oneline`

```bash
git revert edcdf19
```

# Ignorando Arquivos
Podemos criar um arquivo chamado `.gitignore` onde dentro dele podemos especificar os arquivos que devem ser ignorados pelo Git, assim não apareceram no `git status`, se tornando totalmente invisível ao nosso diretório, podemos ignorar diretório inteiros, arquivos específicos, extensão especifica, entre outros

```bash
node_modules/
.DS_Store
*.log
```

>[!note] Removendo Rastreamento de Arquivos
>As vezes podemos esquecer de adicionar um arquivo ao `.gitignore`, e quando adicionamos ele já esta sendo rastreado pelo nosso repositório Git, para resolver podemos utilizar o seguinte comando.
>```bash
>git rm -r --cached .
>```
>Assim removendo todos os arquivos do rastreamento, agora basta adiciona-los novamente através do comando `git add .` que o Git percebera que não ouvi alterações neles, e vai apenas ignorar os arquivos especificados agora no `.gitignore`

# Log
Podemos acessar as informações dos _commits_ através do seguinte comando

```bash
git log
git log --oneline
git log -n 5
git log --since=2020-10-01
git log --until=2020-10-01
git log --author=Wesley
git log --grep="init"  // Expressão regular
```

Possuindo varias flags possíveis que altera a visualização, como a `--oneline` que deixa cada _commit_ em uma linha, com a mensagem do _commit_, porem não traz informação do dono do _commit_, ou seja, dependendo das necessidades.

# Status
Utilizando o comando que traz os dados das alterações no nosso repositório, podemos verificar, em que [[Introdução ao Git#Fluxo Git|estado]] nosso arquivo alterado de encontra, e o tipo de alteração realizada.

```bash
git status
```

# Comparando
Através do seguinte comando.

```bash
git diff
```

Temos acesso as alterações realizadas nos nossos arquivos, onde é exibido linha a linha o que foi removido e adicionado, com as linha removidas sendo iniciadas com o operador `-` e as linha adicionados com o operador `+`, ou seja, mostrara as alterações dos arquivos rastreados, pois, novos arquivos não possui uma versão anterior para alteração.
Quando um arquivo é adicionar a _Stage Area_, ou seja, mudamos seu [[Introdução ao Git#Fluxo Git|estado]] para _Staged_, ele não aparece mais no `git diff` padrão, é necessário adicionar uma _flag_ para mostrar as diferenças apenas dos arquivos que se encontram como _Staged_, ficando da seguinte forma

```bash
git diff --staged
```

>[!note] _Flag_ antiga
>Podemos encontra tutoriais e vídeos antigos que utilizam a _flag_ `--cached`, funciona por enquanto, esse é o nome antigo que era utilizado

# Adicionando Repositório Remoto
Podemos adicionar repositórios remotos onde sincronizaremos nosso repositório do Git local, com um repositório remoto, através do seguinte comando.

```bash
git remote add nomeParaIdentificarRepRemote nomeBranchPrincipal
```

# Enviando para Repositório Remoto
Para enviarmos o ultimo _commit_ para nosso repositório remoto, basta utilizar o seguinte comando

```bash
git push nomeParaIdentificarRepRemote nomeBranchPrincipal
```

Podemos utilizar a _flag_ `-u` para gravar esse repositório remoto como principal assim da próxima vez, será necessário apenas o comando `git push`

# Puxando Alterações
Podemos puxar alterações sofridas no repositório, comando muito utilizado para que trabalha em time com o Git, pois, muitas vezes será necessário sincronizar o as alterações do repositório remoto com o nosso local.

```bash
git pull
```

# Corrigindo Conflitos
Quando esquecer de realizar o `pull` antes de alterar arquivos, ou ocorrer de duas pessoas alteraram a mesma linha, quando tentar fazer o `git pull` ou `git push`, pode ocorrer um erro de conflito, onde o Git não conseguiu realizar o _merge_ automaticamente, assim necessitando de nossa intervenção, Onde será necessário alterar pelo próprio `vim`, simplesmente abrindo o arquivo e encontrando algumas marcações, ou utilizar o `VSCode` que ajuda, disponibilizando botões com escolhas, após resolver o conflito criamos outro _commit_, pois, o Git sempre recomenda criar outro _commit_ em vez de realizar alterações ou apagar _commits_