---
title: Responsividade
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Criando responsividade com styled-components 
---
# 🚀 Introdução
Podemos regras de [[01 - Notes/Code/CSS/Responsividade|responsividade]] facilmente através da [[At-Rules]] _@media_ que podemos adicionar em qualquer componente estilizado por _styled-components_

```js
export cosnt Container = styled.div`
	justify-content: space-between;
	@media (max-width: 390px) {
		justify-content: center;
	}
`; 
```

# Props Responsivas
Propriedade que recebe valores de _breakpoint_ pré-definidos  e possui comportamentos visuais diferentes para cada _brekpoint_.
normalmente criamos um arquivo que exporta um objeto contendo os _brekpoints_, podemos estrutura da forma que desejarmos.

```js
export const brekpoints = [
	{
		name: 'lg',
		media: 1368,
	},
	{
		name: 'md',
		media: 1024,
	},
	{
		name: 'sm',
		media: 700,
	},
]
```

Dentro do nosso componente.

```js
import styled, { css } from 'styled-components';
import breakpoints from '../styles/breakpoints';

export const Box = styled.div`
	width: 300px
	height: 300px;
	border: 2px solid black;
	
	${({ size }) => {
		if(size) {
			return brekpoints.map( breakpoint => {
				if (size[brekpoint.name]) {
					return css`
						@media (max-width: ${brekpoint.value}) {
							width: ${size[breakpoint.name]}px;
							height: ${size[brekpoint.name]}px;
						}
					`;
				}
			})
		}
	}}
`;
```

Basicamente desestruturamos as propriedades pegando a que nos interessa,  em seguida verificamos se a mesma foi utilizada na declaração do componente, se sim retornamos um [[01 - Notes/Code/JavaScript/Manipulando Dados#map|map]] que verifica em cada item da [[Introdução ao JavaScript#Array|array]] de  [[Introdução ao JavaScript#Object|objetos]] se a propriedade possui uma correspondência declara (assim não obrigando declarar todas), caso houver retorna um `css` com os valores.

Utilizando o componentes

```jsx
<Box size={{ lg: 250px, md: 200px, sm: 100px }} />
```

## Refatorando para Função
Invés de reescrever toda essa lógica toda vez que formos utilizar _media queries_, podemos abstrair essa lógica em uma função que recebera como parâmetro a propriedade, e uma [[Assíncronismo#Callback Function|callback]] que será o `css` importando do `styled-components`

```js
function responsiveProp(prop, callback) {
	if(prop) {
		return breakpoints.map( breakpoint => {
			if(prop[brekpoint.name]) {
				return css`
					@media(max-width: ${brekpoints.media}) {
						${callback(breakpoint)}
					}
				`
			}
		})
	}
}
```

Utilizando a função desenvolvida.

```js
import styled, { css } from 'styled-components';
import breakpoints from '../styles/breakpoints';

export const Box = styled.div`
	width: 300px
	height: 300px;
	border: 2px solid black;
	
	${({ size }) => {
		return responsiveProp(size, (breakpoint) => css`
			width: ${size[brekpoint.name]}px;
			height: ${size[brekpoint.name]}px;
		`)
	}}
`;
```