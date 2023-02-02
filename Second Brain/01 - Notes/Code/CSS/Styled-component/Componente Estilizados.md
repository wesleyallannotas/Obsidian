---
title: Componente
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Criando componente com styled-componente 
---
# Introdução
Styled-components geram componentes React que possuem estilos atrelados ao mesmo, assim não ocorrendo colisões de HTML, ou seja, continuar sendo o elemento que escolhemos porem apenas com CSS junto, assim ==mantendo todos os atributos possíveis que o elemento original aceita== para criarmos nosso componente temos que instalar a biblioteca.

```bash
npm instal styled-components

# Tipos do TypeScript
npm install -D @types/styled-components
```

# Criando Componentes

Basta adicionar a importação onde criaremos os componentes.

```ts
import styled from `styled-component`;
```

Criar o nosso componente a partir de um componente base adicionando estilos.

```tsx
export const Title = styled.h1`
	color: black;
	background-color: white;
`;
```

# Estilizando Filhos
Podemos estilizar filhos direto do nosso elemento basicamente adicionando sua tag HTML.

```tsx
export const Title = styled.h1`
	color: black;
	background-color: white;
	a {
		text-transform: none;
		color: inherit;
	}
`;
```

Podemos definir a parentesco entre elementos filhos e pais a vontade.

# Pseudo-Classes
Podemos adicionar estilos as nossas [[Seletores, Combinadores, Pseudo-classes e  Pseudo-Elements#Pseudo-Classes|Pseudo-Classes]], através do caractere de `&`, onde estaremos referenciando ao elementos que estamos no momentos, pode ser usado a mesma ideia para adicionar aos filhos.

```tsx
export const Title = styled.h1`
	color: black;
	background-color: white;
	&:hover {
		color: white;
		background-color: black;
	}
`;
```

Adicionando estilos as pseudo-classes dos filhos

```tsx
export const Title = styled.h1`
	color: black;
	background-color: white;
	a {
		text-transform: none;
		color: inherit;
		&:hover {
			color: tomato;
			font-size: 1.2rem;
		}
	}
`;
```

# Estilizando Icones
Vamos estilizar ícones provindos da biblioteca [React Icons](https://react-icons.github.io/react-icons/),  a sintaxe muda um pouco, foi escolhido o pack de ícones `fi`, um dos vários presentes na biblioteca, basta importar e utilizar o nome do ícone escolhido entre parênteses.

```tsx
import { FiSettings } from 'react-icons/fi';

export const SettingsIcon = styled(FiSettings)`
	color: ${(props => props.theme.colorGrey200)};
	fonts-size: 32px;
	cursor: pointer;
`;
```