---
title: Projeto de Banco de Dados
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: [note, bancoDados]
description: Primeiros passos para projetar um banco de dados.
---
# Projeto  de um Banco de Dados
Vale lembrar que ==projetar um banco de dados esta relacionado com um dos passos para desenvolver um *software*== assim algumas etapas para o desenvolvimento do banco de dados se relacionam com etapas para o desenvolvimento de *softwares*
1. **Levantamento e analise de requisitos:** Entrevista para levantar o problema que deve ser resolvido
	- **Requisitos funcionais:** Relacionado a problemas que o desenvolvimento do *software* ira resolver, partindo normalmente para o desenvolvimento do *UML*
	- **Requisitos de dados:** Levanta as necessidades que o banco de dados ira suprir, ou seja, os dados que terá que armazenar e gerenciar
2. **Projeto conceitual:** Desenvolve um esquema inicial do banco de dados, um **esquema independente** realizando uma abstração do contexto que o banco de dados precisa atender, as entidades do mundo real estarão contempladas com suas características e atributos e suas relações também (Em um modelo de dados de alto nível) ^76305a
	- Analisamos se atendeu os requisitos de dados
3. **Projeto lógico:** (Mapeamento do modelo de dados) Aqui desenvolvemos o **esquema do banco de dados já dependente** de um sistema gerenciado de banco de dados (SGBD), ou seja, obrigatoriamente já estará definido qual **SGBD** ira utilizar, suas entidades se transformam em colunas.
	- Analisamos de atendeu os requisitos funcionais, ou seja, vai atender ao *software* (Esse banco de dados atendera as funcionalidades do *software*?)
4. **Projeto físico:** Onde é criado os **índices** e a criação dos caminhos físicos, ou seja, o desenvolvimento final do banco de dados

# Modelo Entidade Relacionamento
Também definido pela sigla **MER**
- Descreve os dados do mundo real como **entidades, relacionamentos e atributos**
- Cria o modelo [[Projeto de Banco de Dados#^76305a|conceitual]] do banco de dados
- Modelo criado por **Peter Chen** em 1976
- Técnica de modelagem de dados **extremamente difundida**
- Possível criar o diagrama entidade relacionamento representado pela sigla **DER**

## Entidade
Representa um ==objeto concreto ou abstrato do mundo real==, por exemplo:
- Pessoa
- Funcionário
- Venda
- Empréstimo

## Atributos
Propriedade (características) que ==descrevem a entidade==, por exemplo a entidade pessoa pode possuir os atributos:
- CPF
- RG
- Nome
- Idade

# Atributos
- **Domínio:** Esta relacionado qual as definições de quais valores serão aceitos para aquele atributo, por exemplo, no atributo idade só sera aceito números inteiros de ate três dígitos
- **Chaves:** Maneira unica de identificar um valor dentro de um conjunto de entidades, por exemplo definimos uma chave CPF, não é possível duas pessoas com o mesmo CPF, ou seja, dentro desse conjunto  de entidades, ==este valor único não ira se repetir==, para cada entidade é recomendado definir uma chave, exemplos:
	- Pessoa chave CPF
	- Produtos chave código de barras
	- Funcionário chave numero de matricula
A casos onde pode ter mais de uma chave candidata,  ==em outros casos sera necessário criar **chaves compostas** por exemplo para cidade juntar nome + UF==, pois pode existir mesmo nome de cidade em estados diferentes, assim juntando os dois atributos como chave evitamos a repetição

# Representação de entidades e atributos no MER
O atributo ==sublinhado é o escolhido como **chave**==, neste exemplo escolhemos a **entidade pessoa** com os **atributos CPF, RG e nome**
- Pessoa(<u>CPF</u>, RG, Nome)
- Entidades representadas pro retângulos
- Atributos representado por elipses
![[Desenho_BD_MERrepresentaçãoEntidadeAtributo]]

## Atributos Simples e Compostos
- **Atributos Simples ou Atômicos:** São aqueles que não se dividem, por exemplo CPF, RG
- **Atributos Compostos:** Podem ser decompostos para outros atributos por exemplo o atributo endereço pode ser decomposto para Rua, Bairro, Cidade, Numero, UF, CEP)
![[Desenho_BD_MERcompostoESimples|500]]

## Atributos Monovalorados e Multivalorados
- **Atributos Monovalorados:** Possuem um único valor para **cada entidade(Em relação a uma entidade, não para o conjunto de entidades)** por exemplo **Nome.**
- **Atributo Multivalorados:** Podem possuir múltiplos valores para cada entidade por exemplo **Telefone**.
![[Desenho_BD_MER monovaloradosEMúltivalorados|500]]

## Atributos Armazenados e Derivados
- **Atributos Armazenados:** Está armazenado no banco de dados
- **Atributos Derivados:** Podem ser obtidos através de outros atributos ou entidades por exemplo **Idade** que podemos obter através de um calculo simples com a **data de nascimento**
![[Desenho_BD_MERarmazenadosEDerivados|550]]

##  Valores Nulos
Utilizado quando não existe um valor aplicável para um atributo ou quando não é conhecido, por exemplo pessoa com valor nulo para telefone, ou não possui telefone ou não soube informar.

# Relacionamento
É uma associação entre duas ou mais entidades, por exemplo um empregado trabalha em um departamento.
![[Desenho_BD_RelacionamentoBancoDeDados]]
O relacionamento pode ter um conjunto de atributos, por exemplo data de admissão em um departamento (Relacionamento binário).
![[Desenho_BD_MERrelacionamento|550]]
==Relacionamentos são inseridos por meio de **losangos**==, entidade empregado esta relacionado a uma entidade departamento por meio de um relacionamento chamado de trabalha-em, com a relação entre eles possuindo um atributo que no caso é a data de admissão, ou seja, ==os relacionamentos também podem possuir atributos específicos== é possível inserir mais de um atributo, relacionamento binário pois envolve duas entidades apenas.

## Relacionamento Ternário
Envolve três ou mais entidades, por exemplo relacionamento entre empregado, departamento e local.
![[Desenho_BD_MERrelacionamentoTernário|550]]

## Autorelacionamento
Autorelacionamento ou relacionamento recursivo ==envolve duas entidades do mesmo conjunto de entidades==.
![[Desenho_BD_MERautorelacionamento]]
Pois um empregado pode ter a função de supervisionar outro empregado, ou seja, ambos estão no mesmo conjunto de entidades que no caso é empregado.

# Restrições sobre tipos de relacionamentos
- **Razão da cardinalidade:** Determina o numero de relacionamento ao qual uma entidade pode participar (1:1, 1:N, N:M).
- **Participação:** **Determina se a existência** de uma entidade está **condicionado ou não ao seu relacionamento com outra entidade**.
	- **Total:** Uma entidade só existe somente quando ela se relaciona com outra entidade via relacionamento. 
	- **Parcial:** A existência de uma entidade independe dela estar relacionada com outra, tem-se uma restrição de participação entre ambas.
	
## Cardinalidade
Depende muito do contexto para que o banco de dados seria criado.
O exercício para testar e a cardinalidade e assumir um lado como um e relacionar com o outro depois fazer o inverso e pegar os resultados de cada teste.
![[Desenho_BD_MERcardinalidade]]

## Restrição de Participação

![[Desenho_MERrelacionamentoParcialOuTotal|550]]
O departamento só tem sentido em existir se tiver empregados, e os empregados só tem sentido em existir se estiver trabalhando em um departamento.
Já no segundo caso um empregado pode existir sem ser um gerente, agora um departamento precisa de um gerente para existir.

# Entidade Fraca
São entidades que ==não possuem atributo-chave==, só pode ser ==identificada através de associação com outra entidade==, ou seja, por consequência disso ==sempre possui um participação total==, ou seja, dependência existencial, pois, não é possível identificar uma entidade fraca sem a existência da **entidade proprietária**, entidade fraca possui uma chave-parcial, ou seja, junção com atributos de uma entidade proprietária pode gerar uma chave para entidade fraca.
![[Desenho_BD_MERentidadeFraca|550]]
Dependentes de determinado empregado (Filhos, pais), os dependentes só vão existir se existir um empregado.
Chave-parcial é o atributo nome (Sublinhado pontilhado), com sua chave sendo o nome do dependente mais o CPF do empregado.
O relacionamento e a própria entidade tem duas bordas para detonar que é uma entidade fraca.

# Hierarquia de  Classes
Utilizado para criar um relacionamento hierárquico em que as entidades se especializam, por exemplo:
- Funcionário horista e funcionário assalariado (Só funcionário seria o mais genérico)
- Pessoa jurídica e pessoa física
Nome do relacionamento **É-UM**
![[Desenho_MERentidadesGenericasEEspecializadas|550]]
Todo empregado assalariado antes de tudo é um empregado, bem como, todo empregado horista antes de tudo é um empregado, as ==entidades especializadas herdam os atributos da entidade genérica==, nas entidades especializadas ficam aquilo que é mais particular ha aquela especialização.

# Notação para digrama ER
![[Desenho_BD_NotaçãoParaDriagemER|450]]

# Exemplo de Diagrama ER
## Descrição de minimundo
1. A empresa estra organizada em departamento. Cada departamento possui um único nome e um empregado que gerencia o departamento. Temos a data que o empregado começou a gerenciar o departamento. E este pode ter diversas localizações.
2. Um departamento controla um numero qualquer de projetos, cada qual com um único nome, um único número e uma localização
3. Armazenamos o nome de cada empregado, o seguro social, endereço, salario, sexo, e data de nascimento. Um empregado esta alocado em um departamento. Controlamos o numero de horas semanais que um empregado trabalha em cada projeto. Também controlamos o supervisor direto de cada empregado.
4. Queremos ter o controle dos dependentes de cada empregado para fins de seguro. Guardamos o nome, sexo, data  de nascimento de cada dependente e o parentesco dele com o empregado .

## Diagrama desenvolvido no diagrams
> [!attention] Atenção 
> **Faltou atributo nome para o empregado, considere inserido**

![[Diagrama Exemplo.drawio.png]]

# Modelo Relacional
- Criado por Cood em 1970
- Utilizado no desenvolvimento de aplicações
- Necessita do apoio de um SGBD
- Cria o esquema logico do banco de dados
## Exemplo Relação/Tabela Pessoa
![[Desenho_BD_ExemploTabelaPessoa|550]]

## Comparação Modelo Entidade Relacionamento e Modelo Relacional
- Cada entidade se transforma em uma relação (Tabela)
- Os atributos das entidades se transformam em colunas da tabela
- O domínio de cada coluna defini o tipo de dado de cada coluna, por exemplo, campo nome `char(10)` aceitara uma string de 10 caracteres
- Os atributos chave se transformam em chaves primarias da tabela
- Os relacionamentos precisam ser representados
![[Desenho_BD_MERvsModeoRelacional|500]]

# Tipos de dados de atributos (Domínios)
- Numéricos
	- `integer`, `float`, `double`
- Cadeira de caracteres (String)
	- `char` (Dependendo do SGBD aceita colocar quantidade igual `varchar(n)` se não é 1, **char obriga o tamanho especificado**)
	- `varchar(n)` (Aceita qualquer tamanho menor ou igual o limite emposto passado como parâmetro)
- Booleano (`true`, `false`)
- Date (data)
	- `Datetime (data e hora)`
	
## Tipos Chave
- **Primaria:** Formado por ==um ou mais atributos==, deve ser um ==valor único que não se repete== nas outras tuplas da tabela
	- **Simples:** Formado por apenas ==um atributo==
		- Pessoa(<u>CPF</u>,RG, nome) para uma pessoa poderia ser o **CPF** que não se repete
	- **Composta:** Formado por ==mais de uma atributo==
		- Cidade(<u>nome</u>, <u>uf</u>, populacao) para uma cidade utilizamos o nome e o seu estado juntos como chave primaria
- **Estrangeira:** Estabelece a relação entre duas tabelas, a chave primeira de uma tabela se torna uma coluna de outra tabela
![[Desenho_BD_ChaveEstrangeira|550]]

# Restrições de Integridade
São regras que que restringem os valores que podem ser armazenados nas relações (Tabelas também são chamadas de relações)
Um SGBD relacional deve garantir:
- **Restrição de Chave:** Os valores de uma chave primeira deve ser único em todas as tuplas de uma relação
- **Restrição de Entidade:** Chaves primarias não podem ter valores nulos.
- **Restrição de Integridade Referencial:** Mantem a consistência entre as tuplas, estabelece que um valor que faz referencia a outra tupla, esta se referindo a uma tupla existente.

# Transformar um DER em um MR
1. Cada entidade normal do DER será uma relação com os atributos simples.
2. Adicione os atributos simples dos simples dos atributos compostos.
3. Defina a chave primária como um dos atributos chave.
4. Para as entidades fracas, crie uma relação e adicione a chave estrangeira como chave primária da relação.
5. Para cada tipo de relacionamento binário 1:1 (Relação A e B), escolha uma das relações (por exemplo A) para adicionar como chave estrangeira a chave primária da relação B. Caso existem atributos na relação, adicione como atributos em A.
	- É melhor escolher o tipo de entidade com [[Projeto de Banco de Dados#Restrição de Participação|participação total]] em R como sendo a relação S.
6. Para cada tipo de relacionamento binário 1:N (Relação A e B), adicione a chave primário da relação A como chave estrangeira na relação B. Isto porque cada entidade do lado 1 está relacionada a mais de uma estidade do lado N. Caso existam atributos na relação, adicione como atributos em B.
7. Para cada tipo de relacionamento binário M:N (Ralações A e B), ==crie uma nova relação/tabela== R para representar o relacionamento.
8. Adicione como chave primário da relação R as chaves primárias das relações A e B. Caso existam atributos na relação, adicione como atributos em R.
9. Para cada atributo A multivalorado, crie uma nova relação R que inclua o atributo A e a chave primário, K, da relação que representa o tipo de entidade ou o tipo de relacionamento que A como atributo. A chave primária de R é a combinação de A e K.
10. Se o atributo multivalorado é composto inclua os atributos simples que o compõem.
11. Para cada tipo de relacionamento hierárquico, adicione como chave primária  da relação mais especializada a chave primária da relação mais especializada a chave primária da relação mais genérica.

## Convertendo [[Diagrama Exemplo.drawio.png|Diagrama ER]] Para Forma Textual MR
DEPARTAMENTO (<u>número</u>, nome, seguraSocial_Supervisor, dataInicil)
PROJETO (<u>número</u>, nome, localização, numero_Depto)
EMPREGADO (<u>seguroSocial</u>, sexo, nome, dataNascimento, rua, bairro, numero, numero_Depto, seguroSocial_Supervisor)
ASSALARIADO (<u>seguroSocial</u>, salario)
HORISTA (<u>seguraSocial</u>, valHora)
DEPENDENTE (<u>seguroSocial</u>, <u>nome</u>, dataNascimento, parentesco, sexo)
PROJETO_EMPREGADO (<u>numero</u>, <u>seguroSocial</u>, numeroHoras)
LOCALIZAÇÕES (<u>numero</u>, <u>localização</u>)

# Normalização
Normalização é um processo a partir do qual se aplicam regras a todas as tabelas do banco de dados com o objetivo de evitar falhas no projeto, como redundância de dados e dependências ruins.
Existem três formas normais mais conhecidas:
- 1FN - 1ª Forma Normal
- 2FN - 2ª Forma Normal
- 3FN - 3ª Forma Normal

## 1ª Forma Normal
Todos os atributos de uma tabela devem ser atômicos, ou seja, a tabela não deve conter grupos repetidos e nem atributos com mais de um valor.
- **Antes** 
	PESSOA (<u>CPF</u>, NOME, ENDERECO, {TELEFONE}) -> TELEFONE esta entre chaves, pois, possui mais de um valor
- **Depois** 
 PESSOA (<u>CPF</u>, NOME, ENDERECO)
 TELEFONE(<u>CPF</u>, <u>NUMERO</u>)
 ## 2ª Forma Normal
 É preciso estar na 1FM (Primeira Forma Normal já deve estar aplicada). Além disso, todos os ==atributos não chaves da tabela devem depender unicamente da chave primária== (não podendo depender apenas de parte dela).
 - **Antes**
	 ALUNOS_CURSOS (<u>RA</u>, <u>COD_CURSO</u>, NOTA, DESCRICAO_CURSO)
		 **DESCRICAO_CURSO** não tem ligação com o **RA**, ou seja, não depende da chave primária completamente, e sim parcialmente.
- **Depois**
	ALUNOS_CURSOS (<u>RA</u>, <u>COD_CURSO</u>, NOTA)
	CURSOS(<u>COD_CURSO</u>, ==DESCRICAO_CURSO==)
	
## 3ª Forma Normal
É preciso estar na 2FN. Os atributos não chave de uma tabela devem estar ==mutuamente independentes e dependentes unicamente e exclusivamente da chave primária.==
- **Antes**
	FUNCIONARIOS (<u>MATRICULA</u>, NOME, COD_CARGO, DESCRICAO_CARGO)
		**DESCRICAO_CARGO** não depende da **MATRICULA**, é sim do **COD_CARGO**, ou seja, não é dependente da chave primária
- **Depois**
	FUNCIONARIOS (<u>MATRICULA</u>, NOME, COD_CARGO)
	CARGO (<u>COD_CARGO</u>, DESCRICAO_CARGO)
	
## Exemplo Aplicação
- **Antes**
	FUNCIONARIOS_PROJETO (<u>matricula</u>, <u>cod_projeto</u>, horas, nome_funcionario, nome_projeto, uf_projeto, {telefones}, nome_departamento)
- **Após 1FN**
	FUNCIONARIOS_PROJETO (<u>matricula</u>, <u>cod_projeto</u>, horas, nome_funcionario, nome_projeto, uf_projeto, nome_departamento)
	TELEFONES (<u>matricula</u>, <u>numero</u>)
- **Após 2FN**
	FUNCIONARIOS_PROJETO (<u>matricula</u>, <u>cod_projeto</u>, horas,)
	FUNCIONARIOS (<u>matricula</u>, nome_funcionario)
	PROJETO (<u>cod_projeto</u>, nome_projeto, uf_projeto, nome_departamento)
	TELEFONES (<u>matricula</u>, <u>numero</u>)
- **Após 3FN**
	FUNCIONARIOS_PROJETO (<u>matricula</u>, <u>cod_projeto</u>, horas,)
	FUNCIONARIOS (<u>matricula</u>, nome_funcionario)
	PROJETO (<u>cod_projeto</u>, nome_projeto, uf_projeto, cod_departamento)
	DEPARTAMENTO (<u>cod_departamento</u>, nome_departamento)
	TELEFONES (<u>matricula</u>, <u>numero</u>)
