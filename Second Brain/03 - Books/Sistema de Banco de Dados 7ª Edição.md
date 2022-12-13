---
title: Sistema de Banco de Dados 7ª Edição
authors: Abraham SILBERSCHATZ, S. KORTH Henry, F. SUDARSHAN
bookImageUrl: 'https://m.media-amazon.com/images/P/B08H3GFFJP.01._SCLZZZZZZZ_SX500_.jpg'
type: book
completed: false
aliases:
tags: [bancoDados]
description: Tudo sobre sistema de banco de dados dos fundamentos aos novos conceitos
---
# Sistema de Banco de Dados 7ª Edição
![Capa|120](https://m.media-amazon.com/images/P/B08H3GFFJP.01._SCLZZZZZZZ_SX500_.jpg)
# Capitulo 1: Introdução
Um sistema de gerenciamento de banco de dados (SGBD) é uma coleção de dados inter-relacionados com ferramentas/programas para acessar esses dados, provendo uma **solução conveniente e eficiente**, com sua gestão abrangendo a **definição de estruturas e os mecanismos que preveem o compartilhamento entre vários usuários** 
# Aplicação do sistema  de banco de dados
Surgiram da década de 1960, e é usado para gerenciar coleções de dados:
- Altamente valiosas
- Relativamente grandes
- Acessados por vários usuários e aplicações, geralmente ao mesmo tempo
Atualmente os bancos de dados são complexos e a melhor forma de atacar a complexidade é a *abstração*, exemplo do uso da *abstração* é dirigir um carro, você sabe como dirigir e utilizar os controles porem você não entendem o funcionamento detalhado do motor e sim sabe uma *abstração* de  seu funcionamento, com um sistema de banco de dados abstraindo sua complexidade de como guarda e gerencia os dados, facilita para os programadores utilizarem o mesmo, tendo em suas mão os controles mas não sendo necessário conhecer as minucias do funcionamento interno.
Hoje praticamente toda interação que temos online estamos tendo relações com banco de dados.
Em termos gerais, existem dois modos de utilização de banco de dados:
1. Dar suporte ao **processamento de transações onlines**, utilizado por um grande volume de usuários, recebendo pequenos pacotes de dados e realizando pequenas alterações.
2. Dar suporte a **análise de dados**, processar os dados para nortear decisões ou auxiliar a tomada das mesmas, gerando *preditivas* 
# Visão dos dados
Deve fornecer ao usuário uma visão abstrata dos dados, ocultando certos detalhes de onde os dados são armazenados e mantidos.
## Modelo de dados
Apoiando a estrutura de um banco de dados esta o **modelo de dados** que nada mais é uma coleção de ferramentas conceituas para descrever dados, relações de dados, semântica de dados e restrição de consistência.
Eles podem ser classificados em quatro categorias diferentes:
- Modelo relacional
- Modelo de entidade/relacionamento
- Modelo de dados semi-estruturado
- Modelo de dados baseado em objeto
## Modelo relacional
Os dados são representados em formas de tabelas com cada coluna recebendo um único nome, cada linha da tabela representa um pedaço de informação
## Abstração de dados
Buscando o desempenho os cientistas ta computação sofisticaram as estruturas dos dados, assim as tornando complexa onde a maioria dos usuários de banco de dados não as entenderias, assim foi desenvolvido diversos níveis *abstração*, para facilitar a interação dos usuários com o sistema
- **Nível físico:** Desrespeito a como os dados são realmente armazenados, no seu nível mais baixo
- **Nível logico:** O próximo de nível mais alto de *abstração*, descreve quais dados estão armazenados e suas relações, os administradores de banco de dados que precisam decidir os dados a serem armazenados utilizam o nível logico.
- **Nível de visão:** Nível de abstração mais alta, descreve apenas parte do banco de dados, ocultando os dados que não são necessários neste momento, podendo haver mais de um tipo de visão
Os sistemas de banco de dados permitem que utilizando a *abstração* do modelo de dados, e converter as operações abstratas para operações no baixo nível.
![[Desenho;BD;AbstraçãoDeDados]]
A visão (No nível de visão) da secretaria de uma universidade por exemplo oculta o salario dos professores, esta e a idia das diversas visões.
## Instancias e esquemas
O banco de dados muda com o passar do tempo e as interações com o mesmo, instancia esta ligado com como se encontra o banco de dados em determinado momento.
O projeto geral do banco de dados é o esquema
```ad-highlight
O conceito de esquemas e instâncias de banco de dados pode ser entendido por analogia com um programa escrito em uma linguagem de programação. Um esquema de banco de dados corresponde às declarações de variável (juntamente com as definições de tipo associadas) em um programa. Cada variável possui um valor específico em um dado instante. Os valores das variáveis em um programa em um ponto no tempo correspondem a uma instância de um esquema de banco de dados.
```
# Linguagem de banco de dados
O sistema de banco de dados fornece uma **Linguagem de definição de dados(DDL)** e uma **Linguagem de manipulação de dados(DML)** onde ambas não estão separadas, mas sim fazem parte de uma unica linguagem, onde para bancos relacionais a mais famosa é ***SQL***
## Linguagem de definição de dados
Especificamos um [[Sistema de Banco de Dados 7ª Edição#Instancias e esquemas|esquema]] através de um conjunto de definições escritas na linguagem de definição de dados (DDL), onde a mesma também é utilizada para especificar propriedades adicionais dos dados.
Especificamos a estrutura de armazenamento e o método de acesso por meio de um conjunto de instruções especias de DDL chamada de linguagem de armazenamento e definição de dados, onde e definido os detalhes  da implementação do [[Sistema de Banco de Dados 7ª Edição#Instancias e esquemas|esquema]] do banco de dados.
Dados armazenados no banco de dados devem satisfazer restrições de consistência que podem ser definidas por meio da DDL por exemplo definir que o saldo do caixa não possa ser negativo, **a cada atualização as restrições são verificadas**
- **Restrições de domínio:** São as restrições mais elementares pois em uma analogia funcionada como escolher o tipo de uma variável, assim provendo restrições básicas, como não aceitar letras para um campo de inteiro.
- **Integridade referencial:** garantir que o dado que aparece em um capo relacionado, na tabela original exista la.
```ad-example
title: Exemplo
Por exemplo, o departamento listado para cada curso deve ser um que realmente exista na universidade. Mais precisamente, o valor nome_dept em um registro curso deve aparecer no atributo nome_dept de algum registro da relação departamento. Modificações no banco de dados podem causar violações de integridade referencial. Quando uma restrição de integridade referencial é violada, o procedimento normal é rejeitar a ação que causou a violação.
```
- **Autorização:** Esta ligada com a autorização de realizar operações no banco de dados, as mais comuns são autorização de leitura, gravação, inserção, atualização e deleção com usuários podem acumular autorização ou ter apenas uma.
O processamento das instruções do DDL, assim como em qualquer linguagem de programação gera uma saída, onde sua saída é armazenada no **Dicionario de dados** que contem metadados (Dados sobre dados) que só são manipulados pelo sistema, onde antes de qualquer operações com dados reais eles são consultados pelo sistema de banco de dados.
## Linguagem de definição de dados SQL
SQL fornece um DDL poderosa que possibilita a criação de tabelas, com tipos de dados e restrições de integridade.
```sql
create table departamento
	(nome_dept char (20),
	edifício char (15),
	orçamento numeric (12,2));
```
DDL do SQL disponibiliza diversão restrições de integridade como definir uma chave primaria, onde define que outro departamento não poderá ter esse valor.
## Linguagem de manipulação de dados
DML permite acessar e manipular dados conforme organizados pelo modelo de dados apropriado. os tipos de acesso são:
- **Recuperação de informação armazenada no banco de dados**
- **Inserção de novas informação no banco de dados**
- **Exclusão de informações no banco de dados**
- **Modificação de informação armazenadas no banco de dados**
Basicamente existem dois tipos de linguagem de manipulação de dados:
- **DMLs procedurais**: Requer que especifique quais dados são necessários e como obtê-los
- **DMLs declaraticas** (Também chamadas de DMLs não procedurais): Requer que o usuário defina quais dados são necessários sem especificar como obtê-los