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
Por padrão _React Rounter_ 5 realiza o _match_ de rotas, por exemplo um rota `/` e uma rota `/post`, quando acessarmos `/post`, obteremos como resultado o que contem dentro de `/` e de `/post`, comportamento interessantíssimo para sub-rotas, porem para a raiz não é nem um pouco interessante.
Podemos evitar esse comportamento utilizando a propriedade booleana `exact`

# Instalando Biblioteca
Basta instalar a biblioteca `react-rounter-dom` V5 para utilizar o _React Rounter_ para Web.

```bash
npm install react-rounter-dom@5

yarn add react-rounter-dom@5
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

# Params e Query Params
Assim como vimos sobre [[HTTP#Locator (Localização)|URL]] e [[Dados via URL|sobre dados via URL e como consumi-los]], utilizando _Reaact Router_ possuirá a mesma sintaxe para capitação de dados via parâmetros ou query, assim conseguindo capturar e programar em cima disso, por exemplo com determinada URL recebendo determinados dados pelo parâmetro, abri em determinada tela com tais itens selecionados, entre outras diversas ideias.

## Params 
Onde podemos ler esse parâmetro através de um [[#Hooks|hook]] que vem junto com a biblioteca _React Router_, ou seja, interno ao _React Rounter_.

>[!attention] Opcional
>Podemos definir params **opcionais** adicionando `?` no final.

```tsx
<Route path="/production/:selectedProduct?">
	<Product />
</Route>
```

### Redirecionamento Pragmático
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

## Query Params
Podemos obter os query params através de um [[#Hooks|hook]] interno do _React Rounter_, sendo ele o [[#useLocation]], onde dentro do objeto _location_ temos acesso ao query params através da propriedade _search_.
Onde podemos realizar o _parse_ para um objeto JavaScript através de uma interface disponibilizada através da Web API, sendo ela `URLSearchParams`, onde passamos como parâmetro o próprio _search_.

```ts
const location =  useLocation();

const queryParams = URLQueryParams(location.search);
```

Em seguida podemos utilizar o método `get()` para pegar o _query param_ desejado, por exemplo.

```ts
const showStock = queryParams.get('showStock');
```

# Not Found Pages
São páginas que são exibidas quando o usuário acessou uma rota inacessível ou que não existe dentro da nossa aplicação web.
Seguindo a ideia do [[#Switch]] onde não existe o _match_ de rotas, ou seja, renderizando apenas a primeira, basicamente no final da criação das rotas, criamos uma rota com o caminho (_path_) `*`, assim cobrindo todos as outras possíveis rotas, e renderizamos a página que exibira o _Not found_

```tsx
<Switch>
	<Route exct path="/">
		<Redirect to="/production" />
	</Route>
	<Route path="/production" >
		<Production />
	</Route>
	<Route path="*">
		<NotFound />
	</Route>
</Switch>
```

# Protegendo Rotas
Normalmente para tratar de validações de login e permissões entro outros, é **criado um componentes** com o nome `ProtectedRoute`, onde no mesmo é desenvolvido a logica das validações, onde passado, retorna a rota normalmente,  caso negado, retorna para o login ou qualquer outra página.
Para conseguir simplesmente alterar o componentes `Route` padrão para o nosso componente, será necessário pegar os parâmetros e espalhar novamente para o componente que carrega a rota corretamente caso de certo.

>[!tip] Tipagem para o TypeScript
>Para termos a tipagem correta dos parâmetros de um componente `Route`, basta importar `RouteProps`.

```tsx
export const ProtectedRoute = (props: RouteProps) => {
	const token = localStorege.getItem('token');
	
	if (token) {
		return <Route {..props} />;
	}
	return <Route to="/login" />
}
```

Basta utilizar o nosso `ProtectedRoute`

```tsx
<Switch>
	<Route exct path="/">
		<Redirect to="/production" />
	</Route>
	<Route path="/production" >
		<Production />
	</Route>
	<ProtectedRoute to="stock">
		<Stock />
	</ProtectedRoute>
	<Route path="login">
		<Login />
	</Route>
	<Route path="*">
		<NotFound />
	</Route>
</Switch>
```

# Hooks 
São os [[Hooks]] que estão disponíveis dentro da biblioteca _React Router_

## useParams
Através do `useParams` que é um [[Hooks|hook]] da própria biblioteca _React Router_, podemos capturar os valores passados como parâmetros.
Será retornado um objeto contendo os parâmetros, porem uma técnica muito utilizada é a [[Expressões e Operadores#Operadores de Desestruturação|desestruturação]]

```ts
const { selectedProduct } = useParams<ParamsType>();
```

## useLocation
Através do `useLocation` que é um [[Hooks|hook]] da própria biblioteca _React Rounter_, podemos basicamente os valores do objeto `location` encontrado dentro do objeto global do navegador, ou seja, do `window`, por exemplo, recebendo os valores de _hash_, _pathname_, _search_, _state_, onde podemos  capturar os query params através do _search_

```ts
const location = useLocation();
```

## useHistory
Através do `useHistory` que é um [[Hooks|hook]] da própria biblioteca _React Router_, podemos basicamente cuida do histórico da página é uma [[Queue|Pilha]] onde através de tal _hook_ podemos manipular o mesmo.
- `push` - Redireciona para tal caminho da página, adicionando a pilha.
- `replace` - Altera, impossibilita voltar para página anterior, muito utilizado por exemplo para alterar a visibilidade de determinado conteúdo através de _query params_, onde través de adicionar a pila e caso o usuário volte apenas mude a visibilidade, faz mas sentido alterar. 
- `goBack` - Volta para página anterior, voltando na pilha.

```ts
const history = useHistory();
```

## useRouteMatch
Através desse _hook_ temos acesso aos dados da nossa rota para manipular e utilizar da melhor forma, retornando um objeto com os mesmos.

```ts
const routeMatch = useRouteMatch();
```