---
title: Page Layouts
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Possibilidades de construção de layouts.
---
# Introdução
Durante o desenvolvimento da Web passamos por varias formas de construir o layout, ou seja, o posicionamento dos nossos elementos da nossa Web Page.

# Normal Flow
Também chamado de Flow Layout é a maneira que os elementos [[Box Model#Display `block` e `inline`|block e inline]] ficam na página

# [[Tabelas|Table]]
Nos primórdios do desenvolvimento Web a única alternativa para tentar construir layouts era a utilização de elementos HTML `<table>` e manipulações em CSS, além do uso errado do elemento HTML era difícil de dar manutenção e não tinha um resultado tão incrível.

# Tabless
Em sequencia surgiu a ideia de utilizar elementos flutuantes através da propriedade CSS `float`, conseguia um resultado visualmente melhor porem a manutenção era ainda mais complicada, e exigia um conhecimento maior, sobre como flutuar cada elemento e quando usar o `clear`, assim se mantendo e ate aumentando a complexidade da construção do layout

# Frameworks e Grid Systems
Para facilitar o desenvolvimento de layouts foram desenvolvidos frameworks e grid system que buscavam facilitar a construção dos layouts abstraindo diversas dificuldades e facilitando o entendimento e manutenção, porem ainda trazia uma certa dificuldade e a necessidade de depender e estudar um framework

# [[Flexbox]]
Finalmente surgiu ferramentas nativas com a ideia de facilitar a construção do layouts das nossas páginas. Com as propriedades do `flexbox` podemos controlar o comportamento dos elementos HTML dentro de um elemento pai que possui a propriedade CSS `display` com o valor `flex`

# [[Grid]]
Ferramenta também nativa do CSS onde conseguimos construir um Grid e definir o comportamento dos elementos  HTML dentro desse grid, por exemplo quantos espaços de grid esse elementos ira tomar, entre outas funcionalidades.