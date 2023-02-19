---
title: Animação
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Criando animaçòes com Styled-Components 
---
# Introdução
Podemos criar animações facilmente através do uso de `keyframes`, utilizando a mesma sintaxe do CSS normal.

```ts
const Animation = keyframes`
	from {
			transform: rotate(0deg);
	}
	 
	to {
		transform: rotate(360deg);
	}
`;

const Rotate = styled.div`
  display: inline-block;
  animation: ${rotate} 2s linear infinite;
  padding: 2rem 1rem;
  font-size: 1.2rem;
`;
```

# Cuidado
Os quadros-chave são injetados lentamente quando são usados, que é como eles podem ser divididos em código, então você deve usar o auxiliar css para fragmentos de estilo compartilhado
```ts
const rotate = keyframes``

// ❌ This will throw an error!
const styles = `
  animation: ${rotate} 2s linear infinite;
`

// ✅ This will work as intended
const styles = css`
  animation: ${rotate} 2s linear infinite;
`
```
