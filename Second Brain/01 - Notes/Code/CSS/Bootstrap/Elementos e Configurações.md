---
title: Elementos Corretos
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Utilizando elementos
---
# Container
Como boa pratica e para melhor uso do bootstrap é importante que o elemento que abraça todo conteúdo possua a classe `container`
Utilizando `container-fluid` ele pega todo o tamanho disponível.

# Reboot
Basicamente é uma espécie de _reset_ e normalização de estilos CSS para os elementos que são utilizados puramente, ou seja, sem classes para estilizar, existem diversas mudanças, sendo todas encontradas em [Reboot](https://getbootstrap.com.br/docs/4.1/content/reboot/)
Basicamente dita como estão e a melhor forme de utilizar certos elementos que com HTML base trazer uma estilização estranha e tem seu uso perdido.

# Código
Como tratar blocos de código corretamente utilizando elementos HTML no Bootstrap
- `<code>` - Código em linha
- `<pre>` - Código em Bloco
- `<var>` - Indicar variáveis
- `<kbd>` - Indicar entrada de dados via teclado
- `<samp>` - Indicar saída de dados para o usuário

# Figuras
Quando o objetivo for exibir uma imagem com uma legenda atrelada, uma boa pratica e utilizar.
- `<figure>` - Container para abrigar imagem e legenda
- `<figcaption>` - Legenda da Imagem
	- `.text-right` - Alinha texto a direita
- `<img/>` - Imagem
	- `.img-fluid` - Para deixar responsiva
 - `<picture>` - Caso for adicionar mais de um _source_ para a imagem.