---
title: NLWCopa
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [note]
description: Conheicmento adiquirido durante a NLW Copa. 
---
# Introdução
- Fastify - Mini Framework para gerenciar roteamento na aplicação (Muito utilizado o Express).
- Prisma - Utilizado para fazer a comunicação com o banco de dados.
- SQLite - Banco utilizado durante o desenvolvimento (Não é recomendado utiliza-lo na produção, e sim no desenvolvimento, prisma possibilita essa alteração fácil)
- Framework react utilizado sra o Next.js

# Iniciando Back-End
- `npm init -y` - Criando  Package.json
- `npm i typescript -D` - Instalando typescript no projeto
	- `-D` - *DevDependecies* são dependências que vamos utilizar somente em desenvolvimento
		- Sem `-D` são as *Dependecies* que vão para produção
- `npx tsc init` - Criar o setup do typescript
	- Trocar o *target* para `es2020`
- `npm i fastfy` - Instalando o fastify
- Diretório `src` guarda o código
>[!info] Convertendo TypeScript
>Podemos utilizar o comando `npx tsc`, porem repetir esse processo todas as vezes se torna cansativo, para resolver esse problema podemos utilizar a dependência `tsx` obviamente estalando como *DevDependecies* `npm i tsx -D`

## Script Dev
Dentro de `package.json`, apagamos o script teste que vem como padrão e começões criar o nosso script de desenvolvimento.
```json
// ...
"scripts": {
	"dev": "tsx src/server.ts"
	"dev": "tsx watch src/server.ts" // Atualiza em tempo real quando salva
}
// ...
```

## Criando Primeira Rota
Utilizando o Fastify realizamos a criação da primeira rota do nosso back-end
```typescript
import Fastify from 'fastify'

async function bootstrap() {
	const fastify = Fastify({
		logger: true, // Retornar Logs
	})
	
	// localhost:3333/pools/count
	fastify.get('pools/count', () => {
		return { count: 0 }
	})
	
	await fastify.list({ port: 3333, host: '0.0.0.0' })
	// host: '0.0.0.0' para funcionar mobile
}

bootstrap()
```

## Inciando Prisma
- `npm i prisma -D` - Para desenvolvimento, programa em linha de comando que traz algumas funções como criar uma nova tabela.
- `npm i @prisma/client` - Para produção, usado para conectar com o banco de dados.
- `npx prisma init --datasource-provider SQLite` - Pro padrão o Prisma vem configurado para utilizar o postgresql

>[!info] Arquivos Criados
O prisma automatiza o gerenciamento de tabelas, modificamos o arquivo `schema.prisma` e ele se encarrega do resto, prisma é um ORM
>- `.env` - Variáveis de ambiente
>- `schema.prisma` - Onde vão ficar as tabelas do banco

### Criando tabela
No prisma utilizamos o `model` para criar tabela, pois, o prisma funciona tanto para bancos relacionais e não relacionais, por isso optaram por esse nome.

>[!note] Tabela Pool
>Setamos id como **chave primaria**, e utilizamos `cuid()` para gerar strings únicas (invés do `autoIncrement `que é menos seguro)
>```prisma
model Pool {
>	id String @id @default(cuid()) 
>	title String
>	CreatedAt DateTime @default(now())
}
>```
>Utilizamos o  comando `prisma migrate dev` para criar a tabela, utilização `migration` especie de versionamento de banco de dados.

>[!info] Funcionalidade Interessante
>Utilizando o comando `npx prisma studio`, conseguimos **visualizar e interagir** nossas tabelas através do navegado

### Utilizando Prisma
Criamos a constante prisma para realizar as operações

```typescript
const prisma = new PrismaClient({
	log: ['query'], // Exibi todas as querys
})
```

Um exemplo do que o prisma é capaz, como uma **query demanda tempo** para receber a respeita, **temos que utilizar o javascript assíncrono** 

```typescript
// ... Dentro da nossa rota
fastify.get('pools/count', async () => {
	const pools = await prisma.pool.findMany({
		where: {
			code: {
				startWith: 'M'
			},
		},
	});

	return ({ pools });
});
// ...
```

Mudamos a *arrow function* da nossa rota para assíncrona para esperar a resposta da promisse da query.

## Diagram ERD (Automatizado)
Para gerar esses diagramas de forma automática utilizamos `primsa-erd-generator` utilizando o comando de instalação do npm

```bash
npm i prisma-erd-generator @mermaid-js/mermaid-cli -D
# Mermaid gera diagrama através de codigo, assim o prima-erd-generator usa mermaid pro baixo do capo
```

Em seguida para gerar o Diagrama ERD adicionamos ao arquivo do prisma

```prisma
generator erd {
	provider = "prisma-erd-generator"
}
```

Agora basta utilizar o comando `npx prisma generate` que é gerado nosso diagrama automaticamente

## Fastify/Cors
`npm i @fastify/cors`, trás segurança a aplicação definindo quais aplicações estão aptas a consumir o Back-End, passo necessário para o Front-End conseguir consumir corretamente, apos instalar configurar no servidor.

```typescript
await fastify.register(cors, {
	origin: true, 
})
```

Setar `origin: true` Permiti qualquer aplicação acessar o back-End, em produção é comum colocar o domínio da aplicação.

# Iniciando Front-End
O *framework* react utilizado sera o **Next.js** para iniciar um projeto utilizando o mesmo usamos o comando `npx create-next-app@latest -use-npm`
- `.tsx` ou `.jsx` - São arquivos JavaScript ou TypeScript com funções estendidas podendo aceitar tags HTML dentro dele.
- `.jsx` - JavaScript + XML (HTML)
- `.tsx` - TypeScript + JSX
Next.js foi criado com a ideia de trazer o ServerSideRender que por sua vez traz um melhor SEO do site, pois, muitas vezes burla o bloqueamento do javascript o que em uma situação normal não criaria a pagina, pois, o Next.js com react possui a construção da pagina através do JavaScript, ele consegui fazer isso, pois, implicitamente ele traz um **servidor em node**.

## Conectando com o Back-End
Para trazer informação contidas no Back-End, sera **necessário realizar uma conexão HTTP** que sera feita usando a FetchAPI

```typescript
// Dentro de um componente
	fetch('http://localhost:3333/pools/count')
		.then(response => response.json())
		.then(data => {
			console.log(data)
		})
```

Porem com um robô de SEO utilizando um JavaScript desabilitado, essa requisição não sera realizada, para resolver exportamos uma função com o nome `getServerSideProps` ficando da seguinte forma:

```typescript
export const getServerSideProps = async () => {
	const response = await fetch('http://localhost:3333/pools/count');
	const data = await response.json();
	
	console.log(data);
	
	return {
		props: {},
	};
};
```

Para utilizar essas informação basta adicionar `props` como parâmetro para o componente e utilizar suas informações.

```typescript
export default function Home(props) {
	return (
	<h1>Contagem: {props.count}</h1>
	);
}
```

Como estamos utilizando **TypeScript** devemos nos atendar a tipagem, neste caso o criaremos.

# Iniciando Mobile
Com **React Native** criamos APPs nativos, Declarando o que queremos construir onde posteriormente é criado nativamente.
- [Expo](https://docs.expo.dev/) - Facilita o Desenvolvimento polpando tempo com configuração.

# Continuando Back-End
Existem diversas formar de arquitetura de software, ou seja, cordenar a contrução do software, porem utilizaremos uma das mais simples, que é começar pensando pelo Banco de Dados

>[!note] Tabela Pivo
>Como um usuário pode participar de mais de um bolão é necessário criar uma **tabela pivô** para persistir o relacionamento, guardando a informação de quais bolões esse usuário participa (Muitos para Muitos)

>[!note] Campo Nullable (Aceita Nulo como valor)
Utilizando prisma podemos informar que um campo pode aceitar ser nulo adicionando uma interrogação **"?"** após a declaração do seu tipo
>```Prisma
>model User {
>	AvatarUrl String?
>}
>```

>[!info] Curiosidade
>Muitos aplicativos robustos utilizam a ideia de salvar o valor vezes 100 e informando no nome da coluna, assim salvando o valor como inteiro em vez de decimal, por exemplo `priceInCent` um item de 1,79 sera salvo como 179

>[!info] Criando Relacionamento Rapido com Prisma
>Basta adicionar o seguinte texto e salvar
>```
>game Game
>participant Participant[]
>```
>Apos salvar ele criar as seguintes referencias
>```
>model Guess{
>  gameId String
>  game Game @relation(fields: [gameId], references: [id])
>}
>model Game {
>  Guess Guess[]
>}
>```
>Indexando melhor
>```
>@@unique([userId, poolId])
>```

Vamos estruturar o banco criando relacionamentos e melhorando a indexação.

```prisma
model Pool {
	id String @id @default(cuid())
	title String
	code String @unique
	CreatedAt DateTime @default(now())
	ownerId String?
	
	owner User? @relation(fields: [ownerId], references: [id])
	participants Participant[]
}

model Participant {
	id String @id @default(cuid())
	userId String
	poolId String
	  
	guesses Guess[]
	user User @relation(fields: [userId], references: [id])
	pool Pool @relation(fields: [poolId], references: [id]) 
	@@unique([userId, poolId])
}

model User {
	id String @id @default(cuid())
	name String
	email String @unique
	avatarUrl String?
	createdAt DateTime @default(now())
	
	participatingAt Participant[]
	ownPools Pool[]
}

  

model Game {
	id String @id @default(cuid())
	date DateTime
	firstTeamCountyCode String
	secondTeamCountryCode String 
	
	guesses Guess[]
} 

model Guess {
	id String @id @default(cuid())
	firstTeamPoints Int
	seconfTeamPoints Int
	createdAt DateTime @default(now())
	gameId String
	participantId String
	  
	
	game Game @relation(fields: [gameId], references: [id])
	participant Participant @relation(fields: [participantId], references: [id])
}
```

## Criando Seed Banco de Dados
Adiciona dados ficticios no banco de dados principalmente para trabalhar no ambiente de desenvolvimento, criamos um side adicionando um arquivo `.ts` na pasta do prisma com o nome `seed`, conectamos com o prisma (Necessário a importação) `const prisma = new PrismaClient()`, usaremos uma feature muito interessante do prisma que é as **inserções encadeadas para participant**.

```prisma
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();
async function main() {
	const user = await prisma.user.create({
		data: {
			name: 'John Doe',
			email: 'johndoe@gmail.com',
			avatarUrl: 'https://github.com/wesleyallan.png',
		},
	});
	
	const pool = await prisma.pool.create({
		data: {
			title: 'Example Pool',
			code: 'BOL123',
			ownerId: user.id,
		},
	});
	
	const participant = await prisma.participant.create({
		data: {
				poolId: pool.id,
				userId: user.id
			}
		})
}
  
main();
```

Utilizando a feature do prisma para **inserção encadeada** fica da seguinte forma, inserindo o participante junto bom o bolão
- Connect - Conectando com um ja existente
- ConnectOrCreate - Conect se existir se não cria
- Create - Cria um novo registro na tebela

```prisma
const pool = await prisma.pool.create({
	data: {
		title: 'Example Pool',
		code: 'BOL123',
		ownerId: user.id,
		participants: {
			create: {
				userId: user.id,
			},
		},
	},
});
```

>[!info] Dica TimeStemp
>Va no console do navegar e digite `new Date().toISOString()`

Adiconamos o seed no `package.json`

```json
{
	"prisma": {
		"seed": "tsx prisma/seed.ts"
	}
}
```

Executamos o comando `npx prisma db seed`

## Criando `post`
Abaixo do nosso `GET` para a contagem de bolão criamos o nosso `POST`, assim tratando a criação de informação e não apenas um pedido, ou seja, é necessário passar informação para o nosso `POST`
- `request` - Dados enviados
- `reply` - Respota, caso for retornar informação simples basta colocar no return assim não sendo necessário, utilizamos o reply para retornar HTTP status junto.
```typescript
return reply.status(201).send({ title })
```

>[!important] HTTP Status Code
>Importante configurar o HTTP Status Code, ele tráz semantica para as resposta das requisições HTTP, por exemplo código 200 é um código generico de sucesso.

Importante tratar o caso de enviar um informação nula onde não pode, pois, isso pode causar grande problema no banco, ==sempre tratar o dado antes de interagir com o banco==, para isso utilizaremos uma biblioteca para tratar esses possiveis problemas. biblioteca chamda `zod`, após o impormos `import { z } form 'zod'`

```typescript
const createPoolBody = z.object({
	title: z.string(),
	title: z.string().nullable // Caso queira possibilitar o nulo
});

const { title } = createPoolBody.parse(request.body);
```

Vamos utilizar a lib Short Unique ID (UUID) para gerar o codigo do bolão, basta importar e utilizar para gerar um codigo.
```typescript
import ShortUniqueId from 'short-unique-id';
// Dentro do POST
const generate = new ShortUniqueId({ length:6 });
const code = String(generate()).toUpperCase;
```

# Continuando Front-End
Analisar no figma o que são *assets*, posteriormente instalamos o *tailwindcss* no nosso projetoa através do comando `npm instal -D tailwindcss postcss autoprefixer`, após a instalação iniciamos o mesm com o código `npx tailwindcss init -p`, acessamos o arquivo de configuração criado e alteramos o *content* para `['./src/**/*.tsx']` Todos as pastas dentro de `.src` com todos os arquivos terminaods em `.tsx` vão precisar do *tailwind*, sem seguida criamos o arquivo `global.css` dentro da diretorio `style` e importamos o que for necessário ficando da seguinte forma.

```css
@tailwind base;
@tailwind utilities;
@tailwind components;
```

Em seguida importamos o CSS no arquivo `_app.tsx`

>[!info] Arquivo _app.tsx
>Funciona como um arquivo Global, sempre sera carregado junto com todas a paginas.

# Aula 2 : 01:08