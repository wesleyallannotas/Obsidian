---
title: Introdução ao style-component
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Introdução ao maneira de escre CSS styled-component
---
# Introdução
style-component é uma maneira de escrever CSS dentro da stack do JavaScript, basicamente tem seu uso atrelado ao [[Introdução ao React|React]] e React Native, possibilita criar componentes com sua estilização, usando sintaxe do CSS, basicamente escreveremos os estilos dentro de _template strings_ através da ideia de [Tagged Templates)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#tagged_templates).

```js
const Title = styled.h1`
	font-size: ${fontSize};
	text-align: center;
	a {
		color: palevioletred;
		text-decoraton: none;
		&:hover {
			color: #666;
		}
	}
`;
```

# Vantagens
- Resolve o problema de especificidade do CSS, pois o CSS fica encapsulo no componentes não havendo conflito com outros CSS que podem sobrescreve-lo.
- Utilizada a sintaxe padrão do CSS
- CSS-in-JS, não havendo a necessidade de criar arquivos separados
- Sintaxe amigável
- Utilizar a lógica do JavaScript na verificação, podendo definir cores do componente através de valores recebido por [[Componentes#Propriedades|propriedades]].
- Recurso ThemeProvider, onde em sua ideia envelopamos todos os estilos em um theme, como consequência facilitando até mesmo a criação facilidade dos temas _dark_ e _light_

# Desvantagens
- Leitura do código confusa
- Não é possível cachear o CSS
- Performance pode ser afetada, pois é compilado em tempo de execução.
- Debugging