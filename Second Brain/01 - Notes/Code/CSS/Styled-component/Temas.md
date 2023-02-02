---
title: Temas
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Criandos temas com styled-components 
---
# Introdução
Podemos criar temas para o nosso _styled-compoonents_, ou seja, arquivos que conterá objetos com dados para o nosso CSS, existem abordagens diversas, desde objetos com cores numerados pelas forças, a objetos com diversos valores para diversas propriedades.
O importante é que usando `ThemeProvider`, esse objeto contendo os temas ficara disponível para todos os seus filhos.
Assim criando temas com as mesma propriedades mas com valores diferentes, basta mudar o referenciado no ` <ThemeProvider>` que todas as propriedades mudaram dinamicamente.

# Criando Theme
Técnica utilizada para criar temas _light_ e _dark_ por exemplo, porem podemos criar quantos temas quisermos, e muda-los facilmente.

>[!attention] Diferença de Importanção
>Como visto sobre [[Modulos|importação e exportação]] quando utilizamos `exports` antes de declarar, muda a importação, já quando usamos `default` e o que será importando quando não desconstruído.

```ts
// Exeemplo 1
export const theme = {
  colorBlue200: '#0B4F6C',
  colorGray200: '#DCE0D9',
  colorGray100: 'rgba(176, 178, 184, 0.79)',
  colorWhite: '#FBFBFF',
  colorYellow500: '#FFE548',
};

// Exemplo 2
export default {
	title: 'light',
	colors: {
		primary: '#C62E65',
		secundary: '#D63AF9',
		background: `#F5F5F5`,
		text: '#333'
	},
	fonts: {
		size: '16px';
		//....
	}
}

```

Depois basta importar no nosso `App.tsx` e envolver todo conteúdo nele.

```tsx
import { ThemeProvider } from 'styled-components';
import { theme } from './themes/theme'

const App = () => {
	return (
		<ThemeProvider theme={theme}>
			// Conteúdo
		</ThemeProvider>
	)
}
```

Assim ficando disponível para todos components

```tsx
import styled from 'styled-components';
  
export const Title = styled.h1`
  font-family: Roboto;
  font-weight: bold;
  font-size: 28px;
  color: ${(props) => props.theme.colorGrey200};
  padding: 10px;
`;
```

# Tipando Para AutoComplete
Basicamente criamos uma arquivo declaração de tipos e sobrescreve uma definição de tipos presente dentre do `styled-components` através da seguinte sintaxe.

```tsx
// Arquivo styled.d.ts
import 'styled-components';

declare module 'styled-components' {
	export interface DefaultTheme {
		title: string;
		colors: {
		primary: string;
		secundary: string;
		background: string;
		text: string;
		}
		fonts: {
			size: string;
			//....
		}
	}
}
```

Ou podemos mais inteligente e usar da própria linguagem para preencher.

```ts
// Aruivo styled.d.ts
import 'styled-components'
import { light } form './themes/light'

declare module 'style-components' {
	type CustomTheme = typeof light;
	export interface DefaultTheme extends CustomTheme {};
}
```

Em seguida é necessário informar para o TypeScript através do seu arquivo de configuração `tsconfig.json`, para compilar esse arquivo junto com a aplicação, no final basta adicionar.

```json
"files": [
	"src/styles/styled.d.ts"
]
```