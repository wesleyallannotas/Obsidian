---
title: React Rounter
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [react]
description:  Trabalhando com Rotas no React
---
# Introdução
E de extrema utilidade o uso de rotas dentro de nossa aplicação, pois assim podemos gerar URLs que quando acessadas acessaram determinada página com determinado componentes carregando de tal forma, assim possibilitando o acesso direto a tal funcionalidade ou dados especifico.
Utilizaremos da biblioteca [React Router](https://reactrouter.com/en/main) para tal objetivo, sendo possível seu uso tanto na web quanto no mobile.

![[Desenho_React_ReactRounter|600]]

Utilizando as rotas podemos acessar os [[Dados via URL#Parâmetro|parâmetros]] e as [[Dados via URL#Query|pesquisas]], assim podendo carregar dentro do nosso componente, modificando o resultado que pode ser acessado via URL.

## Match de Rotas
Por padrão React Rounter realiza o _match_ de rotas, por exemplo um rota `/` e uma rota `/post`, quando acessarmos `/post`, obteremos como resultado o que contem dentro de `/` e de `/post`, comportamento interessantíssimo para sub-rotas, porem para a raiz não é nem um pouco interessante.
Podemos evitar esse comportamento utilizando a propriedade booleana `exact`

# Instalando Biblioteca
Basta instalar a biblioteca `react-rounter-dom` para utilizar o _React Rounter_ para Web.

```bash
npm install react-rounter-dom

yarn add react-rounter-dom
```

Caso esteja utilizando TypeScript é importante adicionar os tipos.

```bash
npm install -D @types/react-rounter-dom

yarn add -D @types/react-rounter-dom
```

# BrowserRouter
Container que deve abraçar toda aplicação para o funcionamento do React Rounter, ou seja, qualquer interação com React Router deve estar dentro de um componente `<BrowserRouter>`

```tsx
<BrowserRouter>
	<Switch>
		<Route exaxt path="/"><Home /></Route>
		<Route path="/posts"><Posts /></Route>
	</Switch>
</BrowserRouter>
```


# Rotas
Podemos criar rotas dentro da nossa aplicação utilizando do componente `Route`, onde como parâmetros podemos passar o caminho através do `path` e especificar que ele só vai devolver tal conteúdo quando acessado exatamente, evitando [[#Match de Rotas]].

```tsx
<Route exact path="/">
	<Home/>
</Route>
```

# Switch
Garante que somente uma rota seja renderizada por vez, ou seja, quando der _match_, renderiza a primeira e para por exemplo com `/post`, seria renderizado o `/` e pararia.
Porem temos um problema, e como vamos acessar as outras rotas como `/post` por exemplo,  seria necessário adicionar o `exact` no `/` assim não ocorrendo o `match` e chegando ate o `/post`

```tsx
<Switch>
	<Route exact path="/">
		<Home />
	</Route>
	<Route path="/posts">
		<Posts/>
	</Route>
</Switch>
```

# Links
Basicamente é uma ancora `<a>` que se conecta ao _Raact Router_, realiza a mudança de conteúdo sem a necessidade de outras _requests_, ou seja, não recarrega a página e todo seu HTML e conteúdo, através da propriedade `to` podemos especificar para qual rota será enviado.

```tsx
<Link to="/posts">Posts</Link>
```

## NavLink 
Basicamente igual ao `Link`, porem através dele podemos adicionar estilização na rota atual que estamos, pois ele adiciona automaticamente a classe `active`.

```tsx
<NavLink to="/posts">Posts</NavLink>
```

## Estilizar
Ambos podem ser estilizados facilmente através do `styled-components` através da seguinte sintaxe.

```tsx
const export MenuItem = styled(NavLink)`
	text-transform: none;
`;
```

# Redirecionamento
Através do componente `Redirection` podemos criar redirecionamentos para determinadas rotas.

```tsx
<Route exact path="/">
	<Redirecton to="/production" />
</Route>
```

Muito útil quando queremos definir caminhos diferentes para o usuário dependendo do seu estado.

# Parâmetros
Assim como vimos [[Dados via URL|sobre dados via URL]], utilizando _Reaact Router_ possuira a mesma sintaxe para capitação de dados via parâmetros, assim conseguindo capturar e programar em cima disso, por exemplo com determinada URL recebendo determinados dados pelo parâmetro, abri em determinada tela com tais itens selecionados, entre outras diversas ideias.
Onde podemos ler esse parâmetro através de um [[#Hooks|hook]] que vem junto com a biblioteca _React Router_

>[!attention] Opcional
>Podemos definir parâmetros opcionais adicionando `?` no final.

```tsx
<Route path="/production/:selectedProduct?">
	<Product />
</Route>
```

# Redirecionamento Pragmático
Basicamente é um redirecionamento sem o uso de components como `Link`, `Redirect`, utilizaremos do [[#Hooks|hook]] [[#useHistory]]

```ts
const history = useHistory();

const goToProduct = (id: number) => history.push(`/production/${id}`);
```

Invés de criar uma _template string_ manualmente correndo risco de quebrar caso troque a rota no futuro, Podemos fazer de outra forma utilizando o [[#useRouteMatch]] e a função `generatePath` que é interna ao _React Router_ também. basicamente usaremos o `userRouteMatch` para pegar os dados de _match_ da nossa rota e a função `generatePath` para gerar uma nova rota de forma inteligente, ou seja, mesmo alterando no futuro os _paths_ não será necessário vim corrigir as [[Introdução ao JavaScript#Template Strings|template strings]]

```ts
function goToProduct(id: number) {
	const urlToGo = generatePath(routeMatch.path, {
		selectedProuct: id
	})
}
```

# Hooks 
São os [[Hooks]] que estão disponíveis dentro da biblioteca _React Router_

## useParams
Através do `useParams` que é um [[Hooks|hook]] da própria biblioteca _React Router_, podemos capturar os valores passados como parâmetros.
Será retornado um objeto contendo os parâmetros, porem uma técnica muito utilizada é a [[Expressões e Operadores#Operadores de Desestruturação|desestruturação]]

```ts
const { selectedProduct } = useParams<ParamsType>();
```

## useHistory
Através do `useHistory` que é um [[Hooks|hook]] da própria biblioteca _React Router_, podemos basicamente cuida do histórico da página é uma pilha onde através de tal _hook_ podemos manipular o mesmo.
- `push` - Redireciona para tal caminho da página.
- `replace` - Altera, impossibilita voltar para página anterior.
- `goBack` - Volta para página anterior.

```ts
const history = useHistory();
```

## useRouteMatch
Através desse _hook_ temos acesso aos dados da nossa rota para manipular e utilizar da melhor forma, retornando um objeto com os mesmos.

```ts
const routeMatch = useRouteMatch();
```