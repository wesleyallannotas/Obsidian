---
title: Estilos Globais
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Criando estilos globais com styled-components
---
# Introdução
Como sabemos através do _styled-components_ podemos criar estilos para componentes de forma isolada facilmente, porem quando se torna necessário um CSS global, seja para aplicar alguns Resets ou alguns estilos específicos para nosso projeto, fica a duvida de como aplicar.

# Criando Estilo Global
Para resolver este problema temos o `createGlobalStyle`, onde basta importado e atribuir valor ao mesmo através da sintaxe do _styled component_ 

```tsx
import { createGlobalStyle } from 'style-components';

export default createGlobalStyle`
	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}
	
	body {
		background: #F5F5F5;
		font-size: 14px;
		color: #333;
		font-family: sans-serif;
	}
`;
```

# Aplicando
Para aplicarmos basta importar o nosso estilo global no arquivo `app.tsx` e adiciona-lo em qualquer lugar do retorno, normalmente adicionamos no inicio.

>[!tip] Junto com ThemeProvider
>Não tem problema algum utilizar junto com ThemeProvider
>```tsx
>return (
><ThemeProvider theme={theme}>	
<GlobalStyle />>	
</ThemeProvider>
>```

```tsx
import GlobalStyles from './styles/global';

const App = () => {
	return (
		<div className='container'>
			<GlobalStyles />
			// Outros componentes...
		</div>
		
	)
}
```