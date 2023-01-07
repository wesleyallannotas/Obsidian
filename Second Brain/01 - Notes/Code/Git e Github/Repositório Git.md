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

```sh
git init
```

Criando o diretório oculto `.git` que armazena as configurações e o versionamento do projeto.

# Criando Commit
Para criarmos um _commit_ primeiro é necessário armazenar adicionar os arquivos ao _commit_ através do comando

```sh
git add nomearg
git add .
```

Quando utilizamos o `.` é adicionada todas as modificações de uma vez, em seguida utilizamos o comando para criar o _commit_ utilizando a _flag_ `-m` para adicionar uma mensagem ao _commit_

```sh
git commit -m "init"
```

# Log
Podemos acessar as informações dos _commits_ através do seguinte comando

```sh
git log
git log --oneline
git log -n 5
git log --since=2020-10-01
git log --until=2020-10-01
git log --author=Wesley
git log --grep="init"  // Expressão regular
```

Possuindo varias flags possíveis que altera a visualização, como a `--oneline` que deixa cada _commit_ em uma linha, com a mensagem do _commit_, porem não traz informação do dono do _commit_, ou seja, dependendo das necessidades.