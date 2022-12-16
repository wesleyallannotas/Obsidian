---
title: Valres e Unidades de Medidas no CSS
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Funcionamento de valores e unidades de medidas sendo elas absolutas e relativas.
---
# Introdução
Cada propriedade possui valores, seguindo a anatomia `propriedade: valor`, o estudo dos valores aceitos por cada propriedade é constante, pois, além de estar em constante mudança são muitas, nas documentação em inglês podemos encontrar diferentes nomes, sendo os mais comuns:
- *Values*
- *Data-types*

>[!tip] Documentação
>Podemos encontrar uma documentação bem completa e atualizada em:
>-  [MDN Web Docs](https://developer.mozilla.org/pt-BR/)
>- [DevDocs](https://devdocs.io)
>
>Encontraremos o tipo de valores aceitos entre sinais de maior e menor, por exemplo `<color>`

# Tipos Numéricos
Alguns tipos de valores possíveis para algumas propriedades são os tipos numéricos que abrangem:
- `<Integer>` - Número inteiro como {-10, 10, 255...}
- `<number>` - Número decimal {-2,5, 2,5, 255,80, 10, -10...}
- `<dimension>` - É um `<number>` com uma unidade junto, por exemplo {80deg, 2s, 80px, 1.5s}
- `<porcentagem>` - Representa a fração de outro número {25%, 20%, 50.5%}

# Unidades Comuns
- `<length>` - Representa um valor de distância: `px, em, vw`
- `<angle>` - Representa um ângulo: `def, rad, turn`
- `<time>` - Representa um tempo: `s, ms`
- `<resolution>` - Representa resolução para dispositivos: `dpi`

# Distancias Absolutas
São fixas e não alteram seu valor:

| Unidade | Nome               | Equivalência        |
| ------- | ------------------ | ------------------- |
| cm      | Centímetros        | 1cm = 96/2.54       |
| in      | Inches (Polegadas) | 1in = 2.54cm = 96px |
| px      | Pixels             | 1px = 1/96th of 1in |

O mais comum é o **px**, não é recomendado utilizar **cm**

# Distancias Relativas
São relativas a algum outro valor, pode ser elemento pai, root ou ate mesmo o tamanho da tela, por consequência traz uma maior responsividade, se adaptando a diferentes telas:

| Unidade | Relativo a                                   |
| ------- | -------------------------------------------- |
| em      | Tamanho da font do pai                       |
| rem     | Tamanho da font do elemento raiz (root/html) |
| vw      | 1% da viewport width                         |
| vh      | 1% da viewport height                        |

# Porcentagem
Sempre será relativo a algum valor, muitas vezes tratadas da mesma maneira que as distâncias que são identificadas pelo *data-type* `<lenght>`, forma simples de perceber esse comportamento é através da execução do seguinte código:
```html
<!DOCTYPE html>
<html lang="pt_BR">
	<head>
		<meta charset="UTF-8" />
		<title>Teste de Porcentagem</title>
		<style>
			:root {
				font-size: 25px;
			}	
			li {
				font-size: 80%;
			}
		</sytle>
	</head>
	<body>
		<ul>
			<li>Texto 1</li>
			<li>Texto 2
				<ul>
					<li>Texto 2.1</li>
					<li>Texto 2.2
						<ul>
							<li>Texto 2.2.1</li>
							<li>Texto 2.2.2</li>
						</ul>
					</li>
				</ul>
	    </li>
		</ul>
	</body>
</html>
```
Podemos perceber uma diferença no tamanho da fontes das tags `<li>` causado pela herança no elemento pai. pois, a ==porcentagem sempre é relativo a algo==

# Posições
Identificado pelo *data-type* `<position>`, representa um conjunto de coordenadas 2D, sendo elas:
- **Top**
- **Right**
- **Bottom**
- **Left**
- **Center**
É usado para alguns tipos de propriedades para posicionar elementos, por exemplo a propriedade `background-position`, por exemplo:

```css
body {
	background-position: rigth 50px;
	background-position: center;
	background-position: left;
	/* Entre outros */
}
```

>[!warning] Atenção
>Não confundir com a propriedade `position`, estamos falando do *data-type* `<position>`, não da propriedade

# Funções
Podemos utilizar funções como valores para propriedades, pois, [funções no CSS](./Introdução#Funções) recebem parâmetros e retornam o valor processado, assim como foi explicado na introdução

# Strings e Identificadores
- Podemos identificar uma **string** como ==texto envolto em aspas==, um lugar onde é muito utilizado é na propriedade `content` de pseudo-elements, por exemplo:
```css
container::after {
	content: "Ola mundo!";
	color: white;
}
```
- **Identificadores** temos um exemplo bem claro, os nomes de cores, por exemplo `tomato`, `red`, `yellow`, entre outros, por exemplo:
```css
p {
	color: tomato;
	font-size: 30px;
}
```