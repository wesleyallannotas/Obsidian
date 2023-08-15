---
title:  Manipulando dados
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [php]
description: Manipulando dados com PHP. 
---
# 🚀 Introdução
Manipulação de dados é a base para as linguagens de programação, importante saber as ferramentas que possuímos e seus poderes.

>[!attention] Atenção com a saida
>Importante se atentar com a diferença da saída de dado para texto comum e para o HTML.

# 🔤 Strings
String é um tipo primitivo que em sumo é uma cadeira de caracteres, sendo eles, letras, números ou símbolos.
Em PHP possuímos as _strings
- _Single Quoted_ - Aspas Simples.
- _Double Quoted_ - Aspas Duplas, que tem a mesma função que as [[Introdução ao JavaScript#Template Strings|Template Strings]] no JavaScript (Com constantes e retorno de funções a interpolação não funciona, sendo necessário realizar a [[Operadores#Concatenação|concatenação]])
- _Heredoc_ - Com a sintaxe _heredoc_ podemos escrever multilinha utilizando os caracteres que desejarmos, basicamente iniciamos com 3 sinais de menor `<<<` é um nome como identificador que se encontrará no inicio e no final, ou seja, multilinha, porem com comportamento de _double quoted_
- _Nowdoc_ - Diferença entre a _heredoc_ é que adicionamos aspas simples no primeiro identificador, assim sendo uma _string_ multilinha, porem com comportamento de _single quoted_.
 
>[!note] Proteger Caractere
>Podemos proteger um caractere utilizando a contra barra.
>```php
>	<?php echo "$nome \"Minotauro\" $snome"  ?>
>```

```php
<?php
	$nome = 'Wesley';
	
	// Single
	echo 'Olá Wesley';
	
	// Double
	echo "Olá $nome";
	
	// Heredoc
	echo <<< FRASE
	Ola Tudo bem $nome \u{1F596},
		Venho por meio dessa mensagem...
	FRASE;
	
	// Nowdoc
	echo <<< 'FRASE'
	Ola tudo bem Wesley,
		Venho por meio dessa mensagem...
	FRASE;
?>
```

## Escape Sequences
- `\n` - Nova linha
- `\t` - Tabulação
- `\\` - Exibi barra invertida
- `\$` - Exibi cifrão
- `\u{}` - Codepoint UNICODE