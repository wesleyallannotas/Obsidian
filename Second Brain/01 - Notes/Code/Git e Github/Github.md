---
title: Note
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags:
description: 
---
# Introdução
Github é uma ferramenta poderosíssima para compartilhar código e armazenar repositórios [[Introdução ao Git#Git|Git]]  em nuvem, hoje proporciona  cada vez mais ferramentas incríveis para o trabalho em equipe.

# Utilizando Branchs
Normalmente utilizamos _branchs_ para trabalhar em funcionalidades e correções em desenvolvimento, assim mantendo o repositório principal (_main_/_master_) apenas com o código testado e funcional, utilizaremos o comando `chekcout` para navegar entre as _branchs_

## Criando Branch
Podemos criar uma _branch_ através da _flag_ `-b`

```bash
git checkout -b myBranch
```

## Enviando Branch
Utilizamos a mesma sintaxe do `push`, porem agora especificando a _branch_ em vez da principal.

```bash
git push origin myBranch
```

## Realizando o Merge
Podemos realizar o _merge_ entre _branchs_, assim concatenando as duas, muito usado quando o ciclo de vida de uma _branch_ é finalizado, assim seu conteúdo devera ir para a _branch_ principal, por meio de um _merge_, devemos estar na _branch_ que recebera os dados da outra, depois basta executar

```bash
git merge myBranch
```

A branch que teve os dados utilizados no caso a `myBranch` continua existindo.

## Deletando Branchs
Podemos deletar por exemplo a _branch_ que realizamos o _merge_, ou qualquer outro, basta utilizar o comando.

>[!attention]
>Lembre-se de sair da _branch_ antes de tentar apaga-la

```bash
git branch -D myBranch
```

Para pagar no repositório remoto, ou seja, no Github em si, podemos acessar a visualização de _branchs_ e simplesmente clicar na lixeira, ou utilizar o comando

```bash
git push origin --delete myBranch
```

# Puxando Branchs
Utilizando o comando `git branch` temos acesso as _branchs_ locais do nosso repositório, porem utilizando a _flag_ `-a` temos acesso as todas as _branchs_, porem caso seja criado uma nova, precisamos atualizar nosso repositório local para enxergar essas novas _branchs_, para isso utilizamos o comando.

```bash
git fetch
```

Caso for deletado _branchs_ no nosso repositório remoto e queremos pegar essa atualização, devemos utilizar a _flag_ `-p`, assim atualizando os _deletes_ também.

# Protegendo Branch
Quando temos um projeto com muitos colaboradores e normal, ter um responsável por realizar o _code review_ é aprovar e realizar os _merges_, e para que acidentes não ocorram podemos proteger nossa _branch_ através da aba _Branches_ nos configurações (_settings_) do repositório no Github.
Basta adicionar a _branch_ e definir as regras que desejarmos.

# Pull-Request
Nada mais é do que alguém realizar um pedido de subir determinado número de _commits_ contidos em _branch_ para a _branch_ principal, onde dependendo das configurações, o dono do repositório, deve autorizar ou não o `Pull-Request`, caso aceito, será realizado o _merge_.
Através da interface do Github, podemos navegar pelos dados do Pull-Request, podendo verificar _commit_  a _commit_ as alterações realizadas, em outra tela, ver as modificações por arquivos, ou seja, dados relevantes para decisão da aprovação ou não.
Sempre que um Pull-Request não é aprovado de cara, e tem alterações requisitados, é necessário clicar no ícone para pedir uma aprovação novamente, pois, Github entende que uma alteração requisitada pode levar mais do que um _commit_ para ser resolvido.