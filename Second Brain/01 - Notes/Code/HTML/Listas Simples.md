---
title: Listas com HTML
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: [html]
description: Como construir listas no html
---
# Tipos
Dentro do HTML podemos construir listas ordenas e não ordenadas, onde quem defini isso é a tag pai que armazenara como conteúdo os itens da listas

## Pai
A tag pai defini qual lista será, existem dois tipos, ordenadas e não ordenadas.
- `<ol>` - Lista Ordenada
- `<ul>` - Lista não ordenada

## Filhos ou Items
Os itens da lista são identificados pela tag `<li>` sendo a mesma para ordenadas e não ordenadas

# Emmet
Para facilitar a escrita das listas podemos utilizar o emmet para gerar varias tags `<li>` de uma vez, basta digitar `li*5`, assim gerando 5 tags `<li>`

# Exemplo
Lista de ingredientes
```html
<ol>
 <li>4 Ovos</li>
 <li>1 Farinha</li>
 <li>1L de Leite </li>
</ol>
```
