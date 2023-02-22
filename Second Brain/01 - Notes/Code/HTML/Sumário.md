---
title: Sumário
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [html]
description: Criando Sumários 
---
# Introdução
Também conhecido como _toggle list_, basicamente é a ideia de ter um texto que esta escondido dentro de um titulo, onde podemos com um clique "colapsar", ou seja, exibir um texto ou outros elementos. Utilizaremos os elementos `sumarry` e `details` que trabalham em conjunto.

# Utilizando
Muito utilizado para _FAQs_, onde possui uma pergunta e clicando na pergunta, surgi a resposta. Por padrão ele possui um titulo, porem podemos alterar através do `summary`

```html
<details>
	<summary>Sobre mim</summary>
	Sou desenvolvedor web frontend
</details>
```

# Atributos
Utilizando o atributo boolean `open` já iniciara aberto "colapsado".

# Estilizando
Podemos estilizar a seta que identifica o conteúdo como aberto ou fechado através de

```css
summary::-webkit-details-market {
	color: red;
}

details[open] summary::-webkit-details-marker{
	color: blue;
}
```
