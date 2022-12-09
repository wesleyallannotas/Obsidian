---
title: Note
author: Wesley Silva
url: 'https://www.freecodecamp.org/portuguese/news/npm-x-npx-qual-e-a-diferenca/#:~:text=npx%3A%20o%20executor%20de%20pacotes,hospedadas%20no%20registro%20do%20npm.'
book:
type: note
completed: true
aliases:
tags: [note, node]
description: Entenda a difereça entre NPM e NPX
---
# NPM o  gerenciador de Pacotes
O npm, em primeiro lugar, é um ==repositório on-line para a publicação de projetos do Node.js em código aberto.==
Em segundo, ele é uma ferramenta de interface de linha de comando, CLI, que ==auxilia a instalação desses pacotes e gerencia suas versões e dependências.==
Quando os executáveis são instalados por meio de pacotes do npm, ele cria links para eles:
-   instalações **locais** têm links criados no diretório `./node_modules/.bin/`
-   instalações **globais** têm seus links criados no diretório global `bin/` (por exemplo: `/usr/local/bin`, no Linux, ou em `%AppData%/npm`, no Windows)
O mesmo pode ser executado caminhando ate a pasta e o executando, ou adicionando-o ao `package.json` na seção de scripts
```json
{
	"name": "sua-aplicacao",
	"version": "1.0.0",
	"scripts": {
		"seu-script": "seu-pacote"
	}
}
```
Assim o executaremos usando o comando
```bash
npm run seu-script
```
É possível observar que executar um pacote com o npm puro exige um pouco de trabalho.
Felizmente, é aí que o **npx** passa a ser útil.

# NPM o executor de pacotes
Desde a versão [5.2.0](https://github.com/npm/npm/releases/tag/v5.2.0) do npm, o npx vem integrado a ele. Desse modo, ele passou a ser um padrão nos dias de hoje.
O ****npx**** também é uma ferramenta de interface de linha de comando, cujo propósito é ==facilitar a instalação e o gerenciamento de dependências hospedadas no registro do npm.==
Agora, é muito fácil executar qualquer tipo de executável com base no Node.js que você instalaria normalmente por meio do npm.
Você pode executar o comando a seguir para ver se ele já está instalado em sua versão atual do npm:

```bash
which npx
```

Se não estiver, você pode instalá-lo assim:

```bash
npm install -g npx
```

## Executar um pacote instalado localmente com facilidade
Se quiser executar um pacote instalado localmente, tudo o que precisa fazer é digitar:
```bash
$ npx seu-pacote
```
O npx verificará se o `<comando>` ou o `<pacote>` existe no `$PATH` ou nos arquivos binários do projeto local. Se estiver, eles o executarão.

## Executar pacotes que não estavam instalados previamente
Outra grande vantagem é a capacidade de executar um pacote que não estava instalado previamente.
Isso é ótimo porque, algumas vezes, você apenas quer usar algumas ferramentas de CLI, mas não quer instalá-las globalmente somente para fins de teste.
Isso quer dizer que você pode economizar alguns espaço em disco e simplesmente executá-las somente quando precisar delas. Isso também significa que suas variáveis globais ficarão menos poluídas.

# Conclusão
NPM é um gerenciador de pacotes para projetos node.js, por meio dele podemos instalar localmente e globalmente, já o NPX vem com a ideia de executar de forma fácil os pacotes node.js trazendo outras ferramentas mais avançadas como executar sem precisar baixar o pacote, executar através do github e executar versões diferentes.