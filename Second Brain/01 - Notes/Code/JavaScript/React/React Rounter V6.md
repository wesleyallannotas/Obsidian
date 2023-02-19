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

# Atualização 6.0
Na versão6.0 do ReactRouterDOM houveram algumas modificações em suas definições:
- `Switch` - Passou a ser chamado de Routes
- `Route` - A propriedade para renderizar elementos agora se chama `element`
Para exemplificar a utilização do “AS” renomeie o BrowserRouter para Router.
- `Redirection` - E feito através da renderização do elemento `Navigation`
- `replace` - Para manter o histórico limpo, você deve definir replace prop. Isso evitará redirecionamentos extras depois que o usuário clicar novamente.

```tsx
<Route path="/" element={<Navigation to="/produciton" replace />} />
```