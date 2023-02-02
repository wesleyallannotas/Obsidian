---
title: Convenções
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [git]
description: Conveções para o versinamento de projetos
---
# Commits
Uma duvida recorrente entre todos os usuários do Git é como nomear [[Introdução ao Git#Commits|commits]] para o melhor entendimento do grupo de desenvolvedores e de pessoas externas que estão tendo o primeiro acesso ao código, basicamente não existe uma regra em si, porem com o passar o tempo e as tentativas de grandes projetos de criar nomeações padrões, foram desenvolvidas algumas ideia, a mais conhecida e seguida é [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/).
Para facilitar adoção e dinamizar na criação de _commits_ seguindo tal ideia foram desenvolvidas "programas" para agilizar a criação dos mesmo, sendo o mais conhecido o [commitizen/cz-cli: The commitizen command line utility. #BlackLivesMatter (github.com)](https://github.com/commitizen/cz-cli)

>[!tip] Dica
>Podemos instala-lo globalmente ou como dependência de desenvolvimento, vai do nosso gosto.

```bash
npm install -g commitizen

# --- No Projeto ---
# npm
commitizen init cz-conventional-changelog --save-dev --save-exact

# yarn
commitizen init cz-conventional-changelog --yarn --dev --exact

# pnpm
commitizen init cz-conventional-changelog --pnpm --save-dev --save-exact
```

Agora basta executar o comando adicionado ao _git_ local do nosso projeto, e construiremos nosso _commit_ interativamente.

```bash
git cz
```