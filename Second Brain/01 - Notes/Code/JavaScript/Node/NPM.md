---
title: Aprenda Node Package Manage
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [node]
description: Apredendo a utilizar o npm, gerenciador de pacotes node mais famoso.
---
# Introdução
NPM é uma sigla para *Node Package Manage* que nada mais é do que o gerenciador de pacotes de bibliotecas JavaScript, mais precisamente de Node.js, podemos verificar rapidamente se o node esta instalado através do comando que retornaria a versão do nosso node, caso de erro não esta instalado.

```bash
npm -v
```

# Criando um Pacote
Podemos criar nosso próprio pacote através do comando `npm init`, onde  após a resposta das perguntas realizadas, será criando o arquivo `package.json` contendo todas as informações do nosso pacote.

>[!Tip] Criando rápido
>Utilizando a _flag_ `-y` damos "sim" para tudo, cirando com os valores padrão

# Instalando Pacote
Podemos instalar um pacote existem no repositório NPM (_Node package Manage_) através do comando `install` (`i`  é  um alias para `install`), onde sem nenhuma _flag_ instalara com dependência do projeto, caso utilize a _flag_  `-D` será instalado como dependência de desenvolvimento, ou seja, o pacote não ira para a versão final do projeto.

```bash
npm install prisma -D  # DevDependecies
npm install prisma@client  # Dependecies
```

Onde será armazenado as bibliotecas Node dentro do diretório `node_modules` e as organizar realizando o mapeamento das dependências no `package-lock.json`, quando realizarmos uma alteração no `package.json` manualmente podemos **realizar o comando `npm update` para atualizar o `package-lock.json`.**

## Pacote Global
Utilizando a _flag_ `-g` podemos instalar um pacote de forma global, ou seja, para toda maquina, podendo utilizar livremente, não ficando preso como dependência de um projeto

```bash
npm install http-server -g
```

### Localização do `node-modules` Global
Podemos descobrir o diretório denominado para armazenar os pacotes nodes instalados de forma global através do comando

```bash
npm root -g
```

## Instalando Dependências do Projeto
Podemos instalar todas as dependências de um projeto com Node que utiliza NPM como gerenciador de pacotes, utilizando o comando `npm install`, assim instalando todas as dependências informadas no `package.json` e criando o arquivo `package-look.json` com as configurações corretas.

```bash
npm install
```

# Desinstalando Pacotes
Para desinstalarmos pacotes node basta alterar o nome do comando para `uninstall`
```bash
npm uninstall http-server -g
```

# Criando Script
No nosso arquivo `package.json` temos a chave `scripts` que contem um objeto, onde podemos adicionar um nome para uma certa cadeia de comandos.

```json
{
	"scripts": {
		"test": "echo \"Error: no test especifies\" $$ exit 1"
	}
}
```

Criamos o "script" chamado "test" podemos executa-lo através do comando.

```bash
npm run test
```

## Nomes especiais
Possuímos alguns nomes de _script_ especiais que podem encurtar a execução do _script_, o mais conhecido é `start`, onde um `script` com esse nome pode ser executa através do comando simplificado, Ou seja, podemos omitir o comando `run` se desejar.

```bash
npm start
```


# Versões de Pacotes
Podemos verificar os dados referentes a versão do nosso pacote no arquivo `package.json`, onde sente arquivo o a chave tem o nome do pacote e o valor é a versão

```json
{
	"dependecies": {
		"moment": "^2.29.1"
	}
}
```

Significado dos números separados por pontos `major.minor.patch`, ou seja, no exemplo acima:
- _Major_ - 2
- _Minor_ - 29
- _Patch_ - 1

Onde podemos entender essas nomenclaturas de forma bem simplificada como:
- _Major_ - Versão do projeto, alterações que podem uma aplicação caso altere.
- _Minor_ - Alteração que não quebram qualquer aplicação usando a mesma _Major_.
- _Patch_ - Resolução de Bug.

## Controlando Atualização
Analisando o valor que contem a versão do pacote, podemos analisar que existem um sinal antes de informar a versão (No exemplo acima é o sinal de `^`), ele é o responsável por controlar como se dará a atualização desde pacote quando realizar um `npm upgrade`, sendo os seguintes possíveis
- `~` - Atualiza somente o _Patch_
- `^` - Atualiza o _Minor_ e o _Patch_
- **Apenas** `*` - Atualiza tudo para o ultimo, ou seja, _Major_, _Minor_ e _Patch_, quando se utiliza este método, não existe é informada a versão.
- **Sem sinal** - Não atualiza, se mantem preso na versão informada

## Instalando Versão Especifica
Podemos instalar uma versão especifica de uma pacote adicionando o sinal de `@` depois a versão desejada, por exemplo

```bash
npm install moment@1.5.1
```

## Informações Sobre Versões
Através do comando `outdated` ele traz informações da versão atual, a deseja para sair de falhas de seguraça por exemplo, ultima versão lançada, entre outras informações

```bash
npm outdate
```

Por exemplo, caso instalasse o `moment@1.5.1`, no dia 05/01/2023 ele retornaria os seguintes resultado usando o comando.

![[npm-outdated.png]]

Porem utilizando `npm upgrade` não altera o `package.json`, simplesmente muda a versão rodando alterando o arquivo `package-lock.json`.