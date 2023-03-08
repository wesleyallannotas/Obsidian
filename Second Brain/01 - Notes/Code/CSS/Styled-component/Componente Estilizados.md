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

## Tipando Propriedades
Caso for utilizado TypeScript no projeto, será necessário tipar as propriedades que o mesmo ira receber.

```ts
interface TitleProps {
  readonly isActive: boolean;
}

const Title = styled.h1<TitleProps>`
  color: ${ props => props.isActive ? props.theme.colors.main : props.theme.colors.secondary };
`;
```

Ou tempos a opção de passar a tipagem direto dentro do [[Generics]].

```ts
const Title = styled.h1<{ isActive: boolean }>`
	color: ${ props => props.isActive ? props.theme.colors.main : props.theme.colors.seconday };
`;
```

# Alterando Tipo
Podemos alterar o tipo do nosso componente facilmente através de um atributo que todo elemento desenvolvido através do `styled-component` possui, sendo ele `as`, assim mesmo que definirmos uma estilo como utilizando o elemento `div`, conseguimos alterar para um `span` por exemplo.

```tsx
// styles.ts
export const Container = styled.div`
	color: #fafafa;
`; 

// index.tsx
<Container as="span"></container>
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

# Estender Componentes Estilizados
Podemos estender componentes estilizados facilmente através da seguinte sintaxe

```ts
export const DefaultA = styled.button`
	color: ${(props) => props.theme.textColor};
	font-weight: bold;
`;
```

Importando e estendendo.

```ts
import { DefaultA } from './DefaultA';

export const DefaultB = styled(DefaultA)`
	font-size: 1.5rem;
`;
```

Quando utilizarmos um componente estilizado `DefaultB`, possuirá a cor e o peso definida dentro de `DefaultA` e o tamanho definido no `DefaultB`, ==possuímos total liberdade para reescrever o que for necessário==.

```ts
import { DefaultA } from './DefaultA';

export const DefaultB = styled(DefaultA)`
	font-weight: 500;
	font-size: 1.5rem;
`;
```

## Exemplo com Icones
Vamos estilizar ícones provindos da biblioteca [React Icons](https://react-icons.github.io/react-icons/) que no fim devolve SVGs,  a sintaxe muda um pouco, foi escolhido o pack de ícones `fi`, um dos vários presentes na biblioteca, basta importar e utilizar o nome do ícone escolhido entre parênteses.

```tsx
import { FiSettings } from 'react-icons/fi';

export const SettingsIcon = styled(FiSettings)`
	color: ${(props => props.theme.colorGrey200)};
	fonts-size: 32px;
	cursor: pointer;
`;
```

# Estilos Dinâmicos
Aproveitando das liberdades do [[Introdução ao JavaScript#Template Strings|template strings]] podemos definir estilos dinâmicos utilizando código, ou seja, expressões dentro de uma `string`.

```ts
export const Container = styled.div`
	padding: ${(props) => props.width && props.height ? "25%" : "1rem 1.375rem"};
	text-align: ${(props) => props.align || "left"};
`;

export const Button = styled.button`
	background: ${(props) => {
		switch (props.type) {
			case "blue":
			return props.theme.color.blue;
			case "lightGray":
			return props.theme.color.gray200;
			default:
				return props.theme.color.primary;
		}
	}
}`;
```

# Atributos de passagem
Finalmente, é importante lembrar que também é possível passar atributos para nossos componentes estilizados usando `attrs` ao defini-los. Por exemplo, se tivermos integrado o Bootstrap em nosso aplicativo, podemos definir um botão com a propriedade `type` (como fizemos no exemplo anterior), mas desta vez pintar a classe apropriada com base no valor dessa propriedade:  

```ts
const Button = styled.button.attrs({
  className: `btn btn-${(props) => props.type || "primary"}`,
})``;

<Button type="primary" />;
```

```ts
export const ContainerSwitchIcon = styled.div`
	display: flex;
	align-items: center;
	${({ isFull }) => !isFull && css`opacity: 0;`};
`;

export const Text = styled.span.attrs( props => ({opacity: props.isFull ? 1 : 0,}) )`
  opacity: ${({ opacity }) => opacity};
`;

export const Title = styled.span`
	opacity: ${ props => props.isFull ? 0 : 1 };
`;
```

# Adicionando Imagens do Background
Partindo do ponto que nada mais é do que um [[Introdução ao JavaScript#Template Strings|template strings]] se queremos adicionar código  JavaScript dentro, basta utilizar a sintaxe da mesma. `${...}`, assim sendo feito da seguinte forma.

```ts
import folhagem from '../../assets/folhagem.svg';

const export Header = styled.header`
	background: url(${folhagem}) top left no-repeat;
`;
```