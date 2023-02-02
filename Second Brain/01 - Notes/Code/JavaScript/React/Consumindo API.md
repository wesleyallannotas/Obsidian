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