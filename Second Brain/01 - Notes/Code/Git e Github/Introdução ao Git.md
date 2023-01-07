---
title: Introdução ao Git
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [git]
description: Conhecendo o versionar de código mais famoso do mundo o Git.
---
# Introdução
O GIT é um **VCS** que é uma sigla para _Version Control System_ ele é o controlador de versões distribuído mais famoso e mais utilizado, ótimo para projetos desenvolvido em grupo e ate mesmo para projetos individuais, responsável por armazenar todas as alterações realizadas entre os _commits_, e ate mesmo as informações do responsável, possibilitando recuperar alterações desastrosas navegando entre os _commits_, compara código entre _commits_ e muito mais, em suma, protege o seu código e seu projeto como um todo.

# Commits
_Commits_ são pontos na historia, onde ele registra todas as alterações em relação ao ultimo _commit_, podemos navegar entre eles, seja consultando as mudanças ou até mesmo restaurando todo o projeto para um _commit_ especifico.

# Branch
São ramificações como galhos de arvores, onde podemos trabalhar livremente registrando através de _commits_, e quando for incorporado as alterações ao ramo (_branch_) principal é realizado o _merge_

# Configurando o Git
Após instalar o Git na nossa maquina é necessário realizar alguns configurações que serão realizadas via linha de comando através do comando `config`, que permiti atribuir variáveis de configuração, utilizando as seguintes _flags_ nossa configuração pode atingir níveis diferentes.
- `--system` - Todos os usuários
- `--global` - Para todo o sistema do usuário
- `--local` - Para o repositório atual

>[!attention] Sobre Prioridade
>Cada nível sobrescreve os valores do nível anterior, dando preferencia para os níveis mais altos.

```sh
git config --global user.name "Wesley Silva"
git config --global user.email "wesley.allansilva@gmail.com"
git config --global core.editor "code -w" # Caso queira utilizar VSCode como padrão
```