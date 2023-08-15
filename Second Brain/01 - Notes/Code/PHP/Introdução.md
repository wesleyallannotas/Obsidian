---
title: Introdução para o PHP
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [php]
description: Aprendendo o PHP 
---
# 🚀 Introdução
O PHP teve seu inicio em 1994, criado por Rasmus Leardorf nascido na Groelândia o mesmo fez contribuições para o projeto do Apache e do MySQL, inicio como uma ferramenta escrita em C onde teve sua primeira versão em 1995 e se tornou uma linguagem a partir da versão 3 lançada em 1998, onde com a entrada dos irmãos os mesmo inventaram o interpretador do PHP o ZEND assim se tornando uma linguagem.
Versão 1 e 2 era PHP _Personal Home Page_ a partir da versão 3 PHP se tornou _PHP Hypertext Preprocessor_

# ⚙️ Desenvolvimento
PHP é uma linguagem _server side_, ou seja, necessita de um servidor para funcionar, podemos emular um localmente para ambiente de desenvolvimento, existem diversas soluções, porem a mais conhecida é o XAMPP.

# 📝 Codando
Antigamente para adicionar um código PHP dentro do nosso documento HTML era necessário recorrer as tags `<script>` onde no parâmetro _language_ passávamos o valor `php`, porem atualmente não funcionando, sendo o oficial a super tag PHP, ou seja, escrever o código dentro de `<?php ?>`

```php
<body>
	<?php
		echo "Hello World! \u{1F30E}";
	?>
</body>
```

Para escrever podemos utilizar tanto `echo` como `print`, tanto faz, perceba que utilizamos um caractere UNICODE que é um emoji `\u{1F30E}`

## Tags
Durante o tempo de vida do PHP varias formas de executar código PHP foi desenvolvido, muitas não funcionam mais ou necessitam de configurações especiais no servidor.

| Tag        | Nome           |
| ---------- | -------------- |
| `<?php ?>` | super tag php  |
| `<? ?>`    | short open tag |
| `<% %>`    | ASP tag        |
| `<?= ?>`   | short tag php  |

Podemos utilizar a `short tag php` quando vamos utilizar apenas um `echo` ou `print`, dessa forma já executamos direto.

```php
<body>
	<?php echo "Ola mundo!" ?>
</body>

<body>
	<?= "Ola mundo!" ?>
</body>
```

### Informações do Servidor
Podemos acessar as informações do servidor facilmente, resultando em uma tabela com todos os dados, através do seguinte código.

```php
<body>
  <h1>Dados do servidor</h1>
  <?php
    phpinfo();
  ?>
</body>
```

# 🗄️Variáveis e Constantes
Linguagens de programação trabalham de diferentes formas com variáveis e constantes, algumas necessitando declaração e atribuição, e muitas exigindo até tipagem.

## Variáveis
Variáveis no PHP não são declaradas e sim apenas atribuídas, podemos atribuir valor a uma variável com PHP utilizando o sinal de cifram `$`, temos liberdade de reatribuir a qualquer momento.

```php
<?php
	$nome = "Wesley";
	$sobrenome = "Silva";
	// Bloco grande de código
	$nome = "Carlos";
	echo "Muito prazer, $nome $sobrenome"
?>
```

## Constantes
Constantes no PHP são declaradas a partir do operador `const`, por convenção seu nome é todo em maiúsculo, é por não possuir o cifrão não pode ser utilizando dentro de um `echo` ou `print`.

```php
<?php
	const PAIS = "Brasil";
	echo "Muito prazer, $nome $sobrenome! Você mora no pais " . PAIS;
?>
```

## Convenção
- Variáveis de preferencia minúsculo e `camelCase`
- Constantes de preferência maiúsculo e `SNAKE_CASE`
	- `snake_case` se restringe a separar os nomes com underline, o uso de maiúsculos ou minúsculo e ao gosto do usuário.
- Métodos e Atributos `camelCase`

# 🎲 Tipos de Dados
Como toda linguagem de programação nosso objetivo e a manipulação de dados, assim havendo diversos tipos, PHP assim como JavaScript possui tipagem fraca e dinâmica.

## Tipos Primitivos
Tipos de dados primitivos são dados base do PHP possui 3 classes de tipos de dados primitivos.
- Escalares
- Compostos
- Especiais

>[!tip] Dados da variável
>Através da função `var_dump()`, temos acesso ao valor e o tipo da variável
>```php
><?php
>$v = 100;
>var_dump($v); 
>?>
>```

### Escalares
- **String** - Sequencia de números, letras e símbolos, sempre entre aspas.
- **Int ou Integer** - Valor inteiro, ou seja, sem ponto flutuante. (Pode ser hexadecimal,  octal)
	- `0x` - Hexadecimal
	- `0b` - Binário
	- `0` - Octal
	- `3e2` - Mesma coisa que `3 * 10 ^ 2`
- **Float, Double ou Real** - (Real não existe mais a partir da versão 7.4) Valores com ponto flutuante.
- **Boolean** - Verdadeiro ou Falso

### Compostos
- **Array** - Sequencia de valores indexada.
- **Object** - Valores com chave nomeada.
### Especiais
- **Null**
- **Resource**
- **Callabe**
- **Mixed**

# Coerção
Coerção é conversão de um tipo de dado, muito útil nas linguagens de programação, basicamente no PHP adicionamos o tipo desejado entre parênteses depois o valor.

```php
<?php
	$v = (int) "920";
	var_dump($v);
?>
```