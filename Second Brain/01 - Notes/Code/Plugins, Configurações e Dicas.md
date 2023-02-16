---
title: Plugins VSCode
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: 
description: Plugins que utilizo para determinadas funções. 
---
# Plugins
- **Material Icon Theme** - Tema de Ícones
- **Dracula Official** - Tema para VSCode
- **Illusion** - Tema baseado no Dracula, mais escuro
- **Tokyo Night** - Tema para VSCode
- **CodeSnap** - Prints bonitas do código
- **Prettier** - Formatador de código
- **Live Sass Compiler** - Compilador de Sass Css
- **Live Server** - Cria servidor web local
- **DataBase Client** - Acesso a banco de dados via VSCode
- **Thunder Client**
- **ES7+ React/Redux/React-Native snippets**
- **DotENV**
- **Color Highlight**
- **EditorConfig for VS Code**
- **Error Lens **
- **ESLint**
- **Git Graph**
- **Tabnine**
- **Todo Tree**
- **vscode-styled-components**

# Instalando e Configurando ESLint e Prettier
ESlint é um linter para JavaScript, ou seja, analisa o código apontando erros, e caso configurado pode até corrigi-los, muito usado para definir padrões no desenvolvimento, já o Prettier é um formatador de código que normalmente o utilizaremos para executar após o salvamento do arquivo, para formatar segundo o que configuramos, utilizaremos os dois em conjunto para maior ganha de qualidade para o nosso código.
Temos que entender que são programas que possuem o inicio de sua ideia a um bom tempo e que muitas vezes são usados em editores de códigos que não possuem plugins como o VSCode, ou seja, seu core tem o funcionamento perfeito pelo terminal, assim sendo importante entender seu suo natural depois partir para o uso do plugin, vamos iniciar instalando e configurando o ESLint.

## Instalando e Configurando ESLint
Vamos instalar o nosso `eslint` como dependência de desenvolvimento.

```bash
npm install -D eslint
```

Em seguida iniciaremos as configurações, onde será feita uma serie de questionamentos e por fim um recomendação de um _pack_ de dependências, recomendado o uso de JSON para o arquivo de configuração.

```bash
npx eslint --init
```

Instalaremos algumas bibliotecas para auxiliar e melhorar nosso ESLint

```bash
yarn add -D eslint-plugin-import-helpers eslint-import-resolver-typescript
```

Em seguida basta configurar o `.eslintrc`, exemplo de _config_ com TypeScript.

>[!tip] Dica Ignore
>Assim como o `git` possui o `.gitignore` o ESLinte também possui seu `.eslintignore` onde podemos definir diretórios e arquivos que serão ignores pelo ESLinte

```json
{
  "env": {
    "browser": true,
    "es2021": true
  },
  "extends": [
    "plugin:react/recommended",
    // "airbnb-typescript",
    "standard-with-typescript",
    "plugin:@typescript-eslint/recommended",
    "plugin:import/recommended",
    "prettier",
    "plugin:prettier/recommended"
  ],
  "overrides": [
  ],
  "parserOptions": {
  "ecmaFeatures": {
    "jsx": true
  },
  "ecmaVersion": "latest",
  "sourceType": "module",
  "project": ["./tsconfig.json"]
  },
   "plugins": [
    "react",
    "@typescript-eslint",
    // "import",
    "eslint-plugin-import-helpers"
   ],
  "rules": {
    "semi": ["error", "always"],
    "quotes": ["error", "single"],
    "indent": ["error", 2],
    "comma-spacing": ["error", { "before": false, "after": true }]
  },
  "settings": {
    "import/resolver": {
      "node": {
        "extensions": [".js", ".jsx", ".ts", ".tsx"]
      }
    }
  }
}
```

Importante se atentar ao `parseOptions.project` que recebe o arquivo de configuração do TypeScript, e a biblioteca de regras do _airbnb_ que foi instalada via `npm`.
A partir de agora podemos rodas o `eslint` no nosso terminal que nosso código passara pelos testes.

```bash
npx eslint ./src/main.tsx
```

## Instalando e Configurando o Prettier
Vamos instalar nosso `prettier` como dependência de desenvolvimento, junto com bibliotecas para interação com `ESlint`

```bash
npm install -D prettier eslint-config-prettier eslint-plugin-prettier
```

E pronto nosso Prettier esta instalado e podemos executa, onde ele cospe o código formatado.

```bash
npx prettier ./src/main.tsx
```

Importante criar um arquivo de configuração `.prettierrc` para o mesmo em JSON para definir regras na formatação, será de extrema importante para resolver problemas de concorrencia entre `ESlint` e `Prettier`, por exemplo

```json
{
  "singleQuote": true
}
```

## Instalando Plugins
Agora que entendemos e sabemos utilizar de forma nativa o `ESLint` e o `Prettier`, podemos instalar a extensões para o mesmo, onde os erros apontados pelo `ESLint` aparecera como erros no editore também podendo definir a formação após o salvamento no arquivo de configuração do VSCode.

```json
{
  "editor.formatOnSave": true,
  "[typescriptreact, javascriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[css]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
  // "editor.codeActionsOnSave": {     // autocorreção via ESLint
  //   "source.fixAll.eslint": true
  // }
}
```

# Editor Condig
Através do arquivo de configuração `.editorconfig` podemos definir configurações para o nosso editor de ==extrema importante para projetos com desenvolvimento em multiplataforma==, por exemplo corrigindo o código que identifica o final de linha, algo que pode dar conflito entre Windows e sistemas base Unix como Linux e Mac.
Existe um _plugin_ que gera automaticamente esse arquivo, onde podemos fazer pequenas alterações caso desejar.


```editorconfig
root = true
  
[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = false
```



# Gerador de Readme
Se você [conhece o básico do NPX](https://blog.rocketseat.com.br/conhecendo-o-npx-executor-de-pacote-do-npm/), pode utilizar essa [ferramenta](https://github.com/kefranabg/readme-md-generator).

```bash
npx readme-md-generator
```

Rodando esse comando na máquina, ele vai te fazer algumas perguntas e conforme você vai respondendo ela vai criando o conteúdo do README para você.
![[exemplo_readme_generator.gif]]

O gerador de README é bem legal, mas talvez você precise fazer alguns ajustes para melhorar.  **Seja objetivo** ao descrever os caminhos e as decisões tomadas. Evite verbosidade no texto e seja conciso ao apresentar o projeto, como se estivesse apresentando um [pitch](https://www.sbcoaching.com.br/blog/pitch/) dentro de um [Hackathon](https://shawee.io/pt/tag/rocketseat/) ou numa reunião.

# Criando Snippets
Basicamente _snipperts_ são atalhos para código para dinamizar a digitação trazendo maior produtividade e tempo para resolver os reis problemas.
Para criarmos _snippets_ no VSCode, basta acessar o ataho `ctrl + shift + p`, digitar `snippets` acessar a opção de configurar _snippets_ escolher se será global ou local ao _workspace_, escolhemos um nome para o nosso arquivo com o _snippet_ (pode conter mais de um), em seguida descometamos a parte do JSON e alteramos ao nosso gosto.
Basicamente dentro de um JSON, nomearemos e criaremos objetos contendo dados do snipet.

```json
{
  "Nome do Snippet": {
    "scope": "linguagem",
    "prefix": "alias para acessar",
    "body": [
      "codigo;",
      "$2"
    ],
    "description": "descrição do nosso snippet"
  }
}
```

Exemplo de _Snippet_ de _reset_ CSS simples, `\t` para dar um _tab_

```json
  "Reset CSS": {
    "scope": "css",
    "prefix": "resetcss",
    "body": [
      "* {",
      "\tmargin: 0;",
      "\tpadding: 0;",
      "\tborder: 0;",
      "\tbox-sizing: border-box;",
      "\tfont-synthesis: none;",
      "\tfont-size: 100%;",
      "\ttext-rendering: optimizeLegibility;",
      "\t-webkit-font-smoothing: antialiased;",
      "\t-moz-osx-font-smoothing: grayscale;",
      "\t-webkit-text-size-adjust: 100%;",
      "}"
    ],
    "description": "simple reset for css"
  }
```