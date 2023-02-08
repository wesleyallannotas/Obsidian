---
title: Responsividade 
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Responsividade com Bootstrap
---
# Introdução
Utilizando o CSS comum temos acesso as [[At-Rules]] _Media Queries_ e _Media Types_, conseguimos desenvolver _layouts_ responsiva, para diferentes tamanhos de dispositivos, porem com o uso do _framework_ CSS Bootstrap temos formas mais simples de criar _layouts_ responsivos, onde caso não nos agrade, podemos manipular.
Assim como as melhores praticas definidas atualmente pelos desenvolvedores, o bootstrap seguia a metodologia _mobile first_, onde todo _layout_ é pensado primeiramente para o _mobile_.

# Tamanhos do Bootstrap
Seguindo a metodologia do _mobile first_ os _medias_ comparando do menor para o maior, nomeando as classes para os determinados tamanhos da seguinte forma. 
- `xs < 567px`
- `sm >= 576px`
- `md >= 768px`
- `lg >= 992px`
- `xl >= 1200px`

# Adicionando Responsividade
Por padrão _Bootstrap_ utiliza _grid_ com 12 colunas, onde temos que ter isso em mente para construir nossos _layots_, podemos utilizar dos [[#Tamanhos do Bootstrap]] para definir a responsividade, onde é usado daquela regra para definir sua responsividade

```html
<div class="container-fluid">
	<div class="row">
		<div class="col-sm">
			<h1>Bootstrap</h1>
		</div>
		<div class="col-sm">
			<h1>Bootstrap</h1>
		</div>
		<div class="col-sm">
			<h1>Bootstrap</h1>
		</div>
		<div class="col-sm">
			<h1>Bootstrap</h1>
		</div>
	</div>
</div>
```

Ou seja quando for menor que `576px` quebra para linha de baixo, assim controlando a responsividade, ou seja, realocando os elementos.

E podemos definir o quando cada um ira ocupar dentro das 12 colunas do _grid_ do _bootstrap_ adicionando na frente do tamanho de quebra escolhido, por exemplo

```html
<div class="row">
	<div class="col-sm-8">
		<h1>Bootstrap</h1>
	</div>
	<div class="col-sm-4">
		<h1>Bootstrap</h1>
	</div>
</div>
```

# Push Down
Podemos utilizar do efeito do _push down_ para definir mais regras de forma simples para responsividade

```html
<div class="container">
  <div class="row">
    <div class="col-6 col-md-6">
      <p>Conteúdo</p>
    </div>
    <div class="col-6 col-md-2">
      <p>Conteúdo</p>
    </div>
    <div class="col-6 col-md-2">
      <p>Conteúdo</p>
    </div>
    <div class="col-6 col-md-2">
      <p>Conteúdo</p>
    </div>
  </div>
</div>
```

Assim tendo seu comportamento da seguinte forma, quando menor que `768px`, como definimos 24 colunas, ou seja, o dobro das 12, quando preenche as doze ele joga o resto caso houver para baixo, ou seja, quando ocorrer a cabre definida pelo `md` obteremos duas linhas com 2 `<div>` em cada.
Podemos definir quantos pontos de quebra for necessário.

```html
<div class="col-12 col-sn-6 col-md-2"></div>
```