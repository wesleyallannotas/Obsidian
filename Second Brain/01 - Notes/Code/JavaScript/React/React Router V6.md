---
title: React Rounter V6
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [react]
description: Criando rotas dentro do React
---
# Introdução
Buscando uma melhor estruturação do projeto e trazer melhorias de performance, foi implementado a versão 6 do _React Router_ onde por se tratar de um _break_, necessita de uma reescrita do código.

>[!info] Tipos
>A nova versão do _React Router_ traz com sigo os tipos, não sendo necessário instalar `@types/react-router-dom`

Basicamente na versão 6.0 do _React Router_ houveram algumas modificações em suas definições:
- `Switch` - Passou a ser chamado de `Routes`
	- Necessita de 
- `Route` - Agora utilizamos uma propriedade chama `element` para renderizar os componentes, invés de passar como _children_
	- `exact` - Com o retrabalho da biblioteca foi abolido a propriedade `exact`
- `Redirection` - E feito através da renderização do elemento `Navigation`
	- `replace` - Para manter o histórico limpo, você deve adicionar a propriedade booleana `replace` . Isso evitará redirecionamentos extras depois que o usuário clicar novamente.

```tsx
<Route path="/" element={<Navigation to="/produciton" replace />} />
```

# Routes
O antigo `Swtich` agora se chama `Routes`, uma de suas grandes mudanças é a necessidade de que seus filhos sejam `Route` puro, assim necessitando de mudanças na ideia de criar um login, como vimos no [[React Router V5#Protegendo Rotas|Protegendo Rotas]].
Assim sendo necessário reescrever e repensar o funcionamento do nosso elemento.
Basicamente mudaremos para receber nosso elemento através de `children` e caso passe na autenticação retorna o elemento, caso não, redireciona para o _login_, e agora nosso `ProtectedRoute` e pai do elemento `Stock`.

```tsx
// Antes
<ProtectedRoute path="/stock">
	<Stock />
</ProtectedRoute>

// Agora
<Route path="/stock" element={
	<ProtectedRoute>
		<Stock />
	</ProtectedRoute>
} />
```

# Route
Uma mudança muito interessante é que ==filhos de rotas, tem que ser rotas== elementos que serão carregados ficam dentro da propriedade `element`, e ==todas as rotas são relativas== trazendo uma semelhança com a ideia de caminhar por diretórios.

# Link
Com a ideia de rotas relativas é a possibilidade de navegar através da utilização da sintaxe de navegação de diretórios, o `Link` ganhou muito mas força, sendo capaz de pro exemplo de forma simples realizar o mesmo resultado da lógica para [[React Router V5#Redirecionamento Pragmático|redirecionamento pragmático]] porem em uma linha, sem a necessidade e _hooks_.

```tsx
<Link to={`../${product.id}`} />
```

# Params e Query Params
Com mudança de _hooks_ e da forma de como navegar entre as rotas, se torna extremamente necessário e obrigatório, a total refatoração nas formas de como utilizar os _params_.

## Params
Agora não é mais necessário a interrogação para se tornar opcional, pois, rotas são relativas, basicamente criamos uma rota para o parâmetro.

```tsx
// Antes
<Route path="production/:selectedProduct?">
	<Production />
</Route>

// Depois
<Route path="production">
	<Route path=":selectedProduct" element={<Production />} />
	<Route element={<Production />} index />
</Route>
```

Basicamente ele verificara que a rota pai não possui um elemento base, vai entrar nos filhos, caso tenha parâmetro vai renderizar tal elemento, caso não tenha passa para o próximo, onde com o atributo booleano `index` é identificado como o _index_, o renderizando.
Poderíamos também possuir componentes separados, assim renderizando a receita quando possuir um parâmetro utilizando o `Outlet`, porem dessa forma também é funcional.

## Query Params
Basicamente utilizando da ideia de navegar pealas rotas de forma relativa, podemos alterar nossa [[HTTP#Locator (Localização)|URL]] atual facilmente através do _hook_ [[#useNavigate]], sendo importante ativar o `replace` para não adicionar diversas URLs desnecessárias no histórico.

```tsx
const toggleVisibility = () => {
	navigate(`?showStock=${!showStock}`, { replace: true });
}
```

# Outlet
Injetando componente filho no elemento pai, através de [[#Route]], realizando o _match_, basta adicionar o componente `Outlet` encontrado dentro da próprio _React Router_, que é onde será injetado o elemento filho.

```tsx
<Route path="/production" element={<Production />}>
	<Route path=":selectedProduct" element={<Recipe />} />
</Route>
```

Agora dentro do elemento pai, ou seja, `Production`, utilizar o `outlet` para especificar onde será injetado.

```tsx
export const Production = () => {
  return (
    <div>
      <S.Title>O que você vai fabricar hoje</S.Title>
      <S.ProductsContainer>
        {data.products.map(product => (
          <S.ProductContainer to={`./${product.id}`} key={product.id}>
            <S.ProductImage src={product.image} alt={product.name} />
            <h4>{product.name}</h4>
          </S.ProductContainer>
        ))}
      </S.ProductsContainer>
      <Outlet />
    </div>
  );
};
```

# Hooks
Houve mudança nos [[Hooks]] também, tanto no nome como no funcionamento.
- `useHistory` -> `useNavigate`
- ❌ `useRouteMatch` 

## useNavigate
Através do _hook_ `useNavigate` podemos navegar pelas rotas, porem agora sem a necessidade de utilizar um método como `push()`

```tsx
const navigate = useNavigate();

// Antes
navigate.push(urlToGo);

// Agora
navigate(urlToGo);
```