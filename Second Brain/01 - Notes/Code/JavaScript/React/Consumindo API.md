---
title: Consumindo API
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [react]
description: Consumindo API com Reacte
---
# Axios
Como vimos sobre [[Requisições#Axios|Axios]] podemos construir e executar requisições HTTP de forma rápida e fácil, e podemos melhorar sua abordagem ao utiliza-lo no React.
Uma boa ideia e criar uma basta `service` dentro do `src` para guardar as configurações inicias da nossa conexão, como uma _base url_.

```tsx
// src/services/api.ts
import Axios from 'axios';

export const Api = Axios.crete({
	baseUrl: 'http://localhost:3333',
})
```

Em seguida dentro da pasta nosso componentes que realizara as requisições criamos um arquivo `services.ts`. onde as criamos.

```tsx
import { Api } from '../../services/api';

export const getFuel = async () => {
	const request = await Api.get('fuel');
	
	return request.data;
};
```

Para consumir o `getFuel` por se tratar de side effect, é necessário o uso do hook [[Hooks#useEffect|useEffects]], onde dentro dele podemos utilizar o `getFuel` através da sintaxe de [[Assíncronismo#Promise|Promise]].

```tsx
// Promise
useEffect( () => {
	getFuel().then(data => data);
}, [])
```

Ou podemos criar uma função com a sintaxe [[Assíncronismo#Async/Await|Async/Await]]

```tsx
// Async/Await
  async function FetchAndUpdateData() {
    const data = await getFuel();
    setFuels(data);
  }
  
  useEffect(() => {
    FetchAndUpdateData();
  }, []);
```

# ⚛️ React Query
React Query ou seu novo nome TanStack Query é uma biblioteca React que permitir gerenciar os dados provindos de requisições, a ideia e gerenciar os dados o estado em si e não tratar da obtenção, podendo utilizar websock, graphQL.

## Iniciando
É necessário adicionar um Wrapper chamado `QueryClientProvider` onde dentro dele podemos utilizar o `react-query`, normalmente ele é adicionado em volta de toda aplicação dentro do próprio `main` ou `app`.
Dentro do _provider_ podemos definir configurações globais, podemos utilizar as padrões que já são boas também, porem um atributo não é opcional que é o `cliente`, para resolver basta instanciar com `QueryCliente` que também deve ser importado.

```tsx
const client = new QueryClient();

ReactDOM.render(
	<React.StrictMode>
		<QueryClientProvider client={client}>
			{...}
		</QueryClientProvider>
	</React.StrictMode>
);
```

## Requisição
É importante lembrar que o `react-query` não realiza requisição HTTP, justamente por sua proposta, então normalmente criamos uma função que realiza o mesmo, e para usar tal requisição utilizamos `useQuery()` hook interno da biblioteca.

>[!attention] Importante sobre _key_
>Sempre definir uma `key` para a _query_, o mesmo serve para identificar o recurso dentro da _store_ global, esse `key` pode ser composta adicionando os valores dentro de uma _[[Introdução ao JavaScript#Array|array]]_, resultando em algo que não se repete.

Assim passando como parâmetro uma `key` e a função que realiza a requisição, sendo uma [[Funções#Arrow Function|arrow funciton]] geralmente.

```ts
async function fetchProducts(id: string) {
  const request = await axios.get(`http://localhost:3333/products/${id}`);
  return request.data;
}

// {...Dentro do componente...}
const query = useQuery(['products', id], () => fetchProducts(id));
```

Invés de jogar tudo dentro de uma única constante ou variável, podemos [[Expressões e Operadores#Operadores de Desestruturação|desestruturar]].

```ts
const { data, isLoading } = useQuery(['products', id], () => fetchProducts(id));
```

### Cache
React Query, revalida a requisição e caso não aja alteração não faz outra requisição, levando a mais performance e economia de recursos. porem podemos forcar um tempo sem realizar outra requisição passando como ==terceiro parâmetro== um objeto de configuração, onde no atributo `staleTime` podemos setar o tempo em milissegundos.


```ts
const { data, isLoading } = useQuery(['products', id], () => fetchProducts(id), {
	staleTime: 10000,
});
```
