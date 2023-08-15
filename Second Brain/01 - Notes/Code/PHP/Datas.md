---
title: Data no PHP
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [php]
description: Trabalhando com datad no PHP
---
# 🚀 Introdução
Trabalhar com datar é essencial para qualquer linguagem de programação, podemos acessar a data atual através da função `data()`, passando letras minúsculas é o número e maiúsculas é escrito, ou seja, por exemplo no dia 04 que cai em uma terça-feira

`date("d")` - Resultado no número do dia, `04`
`date("D")` - Resulta no dia escrito `Tue`

# 🕰️ Alterando TimeZone
Podemos alterar o TimeZone do servidor dentro do código a ser executado através da função `date_default_timezone_set()`, passando a informação do TimeZone a ser seguido.

```php
<?php
	date_default_timezone_set("America/Sao_Paulo");
?>
```