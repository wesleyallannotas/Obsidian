---
title: Operadores PHP
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [php]
description: Os operadores do pHP
---
# 🚀 Introdução
Operadores são um assunto vasto dentro de uma linguagem de programação, com muitos se repetindo entre as diversas linguagens, porem existem divergências.

# Concatenação
Concatenação nada mais é do que a junção de texto, onde no PHP o escolhido para tal função é o `.`

```php
<?php
	echo "Curso" . "PHP"
?>
```

# Coalescência Nula
Assim como no JavaScript o operador de [[Expressões e Operadores#Operadores Lógicos (Logical Operators)|operador de coalescência]] servi para utilizar o da direita quando o da esquerda for nulo.

```php
<?php
	$nome = $_GET["name"] ?? "Não informado";
	echo "Ola $nome";
?>
```

Ou seja, se a **Super Global** `$_GET` não possuir valor para o atributo `name`, assim resultando em nulo, o valor será um _string_ `Não informado`.