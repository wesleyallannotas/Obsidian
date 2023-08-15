---
title: Formulários
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [php]
description: Trabalhando com formulários no PHP 
---
# 🚀 Introdução
Trabalhando com formulários é algo básico para web, com PHP temos que nos atentar mais a configuração do nosso elemento `form` passando o atributo `mwthod` e o `action` corretamente, vale lembrar que no `action` referenciamos quem vai receber tal dados.

```html
<form method="get" action="cad.php">
{...}
```

# 📥 Recebendo Dados
Dentro do nosso arquivo PHP receberemos tal dados através das variáveis **Super Globais**, sendo:
- GET - Variável `$_GET`
- POST  - Variável `$_POST
- Junção `$_GET`, `$_POST` e `$_COOKIES` - Variável `$_REQUEST`