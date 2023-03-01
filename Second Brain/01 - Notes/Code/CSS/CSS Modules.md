---
title: CSS Modules
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: CSS Modules no React 
---
# 🚀 Introdução
Podemos adicionar CSS nativo na nossa aplicação _[[Introdução ao React|React]]_ através do arquivo `index.css`, muito utilizado para _resets_ e aplicação de estilos globais, porem muitas vezes se faz necessário o uso de CSS especifico para cada componente, assim não conflitando com CSS de outros componentes, e de quebrar separando em arquivos isolados facilitando a manutenção, para isso temos _CSS Modules_.

# 🏗️Criando
Por conversão são nomeados da seguinte forma, `Componente.module.css`, e são criados dentro da pasta do componentes, basicamente escreveremos CSS comum dentro do arquivo.

>[!fail] Não pode
>Não pode criar classes com traço `-`, utilizar camalCase ou underline.

```css
/* Login.module.css */
.container {
	display: flex;
	flex-direction: column;
	gap: 2rem;
}

{ ... }
```

# ✨Utilizando

Para utilizarmos nosso _CSS Module_ basta importar o arquivo dentro do nosso componentes _[[Introdução ao React|React]]_ e utiliza-lo como um objeto, com suas propriedades sendo as classes CSS.

```jsx
import styles from './Login.module.css';

export const Login = () => {
	return (
		<div className={styles.container}>
			{ /* Outros componentes */ }
		</div>
	)
}
```

Adicionando as classes criadas no nosso _CSS Module_, podemos perceber que no resultado final o nome da classe é alterado, adicionando caracteres para torna-lo único, não conflitando com outros, por exemplo em um componente que tem uma classe `title` mesmo  possuindo uma classe do mesmo nome em outro componente não vai conflitar, pois, por baixo dos panos não será simplesmente `title` o nome da classe, será por exemplo `_title_qb9s3_12`