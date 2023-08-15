---
title: Regex no JavaScript
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [javascript]
description: Entenda o Regex no javascript.
---
# 🚀 Introdução
Basicamente Regex ou também conhecido como expressões regulares são usadas para validações de valores e até mesmo para alterações junto com o `replace()` dos mesmo, um uso muito comum é para validação de email, cpf, cep, entre outros.

>[!attention] Diferentes Tipos
É importante entender que nem todo Regex é igual, possuindo particularidades entre eles, principalmente entre as linguagens de programação.

# 🏗️ Estrutura
Para ser entendido como uma expressão regular, ou seja, Regex no JavaScript, é necessário que o mesmo se encontre entre barras. `/ ... /`.

- `/\d{...}D/` - d minúsculo pega todos os números, D maiúsculo pega tudo que não é numero.
- `/{...}/g` - Global, analisa  toda cadeia de caracteres, caso não possua, para no primeiro.

# ✅ Validação
O uso principal do Regex é para validação de dados, onde no Javascript podemos armazenar a expressão em uma variável ou lançar diretamente
# ♻️ Alterando
O Regex é poderoso quando usado em conjunto