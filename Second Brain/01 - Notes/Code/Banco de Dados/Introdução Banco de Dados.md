---
title: Introdução Banco de Dados
author: Wesley Sivla
url: 
book: Sistema de Banco de Dados 7ª Edição
type: note
completed: true
aliases:
tags: [note, bancoDados]
description: Ideia de utilidade de banco de dados
---
# Ambientação
No mundo moderno que vivemos hoje estamos cada vez mais imersos em dados, dados estão por todos os lados e em todas tarefas que executamos, diante disto, as ==empresas e interessados buscam interpretar e utilizar esses dados da melhor forma==, e para melhor organização e utilização destes dados coletados, os mesmos tem seu seu armazenamento realizado em bancos de dados.

# Definição
**É um repositório sistêmico de dados relacionados a algo e estruturado afim de atender a demanda do cliente deste tal banco.**
Por exemplo para um aplicativo de relacionamento não interessa que no seu banco de dados guarda o número do seu RA da faculdade.

## Diferença entre dados e informação
 - **Dado:** Valor cru, sem um significado profundo ou relacionamento com outros dados.
	 - Nome
 - **Informação:** Geradas a partir de dados e que traz valor e tem importância para o dono do banco
	 - Nome dos moradores de Osvaldo Cruz

#  Arquivos comuns
Migrando do sistema tradicional analógico de armazenamento em arquivos metálicos separados por pastas contendo os registros, para o digital, foi encontrado alguns problemas decorrente do uso de arquivos comuns que são eles
```ad-fail
title: Problemas na utilização de arquivos comuns

- **Redundância** e **inconsistência** dos dados
	```ad-example
	title: Exemplo
	Registro que representa a ==mesma pessoa em arquivos diferentes== podem ser ==alterados individualmente== causando uma incosistencia.
- **Dificuldade no acesso** dos dados
- **Isolamento** dos dados
- Problemas de **integridade**
- Problemas de **atomicidade**
	```ad-example
	title: Exemplo
	A transferencia de dados deve ser atômica, ou ocorre em sua totalidade ou não deve ocorrer.
- Anomalias de **acesso concorrente**
	```ad-example
	title: Exemplo
	Impossibilidade do acesso simultâneo
- Problemas de **segurança**
	```ad-example
	title: Exemplo
	Impossível delimitar níveis de acesso
```
Diante destes problemas encontrados e a **importância dos dados** no mundo atual, se torna necessário usar uma ferramenta mais focado para combatar esses problemas encontrados e facilitar a utilização, manipulação e armazenamento.
# Sistemas Gerenciadores de Banco de Dados (SGBD)
*Softwares* que tem seu focado em solucionar os problemas da gestão de dados, com diversas ferramentas que trazem comodidade e facilidade na gestão dos mesmos.
## Alguns SGBDs
- [Microsoft SQL Server](https://www.microsoft.com/pt-br/sql-server/sql-server-downloads)
- [MySQL](https://www.mysql.com)
- [ORACLE](https://www.oracle.com/br/database/)
- [PostegreSQL](https://www.postgresql.org)
- [MariaDB](https://mariadb.org)
- [MongoDB](https://www.mongodb.com)
- [FireBird](https://firebirdsql.org)
```ad-check
title: Vantagens do uso de SGBDs
- Compartilhamento de dados
- Controle de acesso
- Pradronização dos dados
- Backup e restauração
- Eliminação de redundância
	```ad-attention
	title: Ateção
	Caso bem estruturado
- Controle de transações
- Restrições de integridade
- Independência dos dados
- Eliminação de incosistência
```
# Arquiteturas de Banco de Dados
## Arquitetura Local
- O banco de dados se encontra no mesmo dispositivo que o usa
- **Normalmente não é um SGBD**
![[Desenho;BD;ArquiteturaLocal]]
## Arquitetura Cliente Servidor
- Utilizado pela maioria das instituições
- O banco de dados se encontra em um servidor
- Vários dispositivos diferentes o acessam
- SGBD responsável por processar as operações com os dados 
![[Desenho;BD;ArquiteturaClienteServidor]]
## Arquitetura Cliente Servidor WEB
- Utilizado pela maioria dos sites
- Cliente do banco sera o Servidor Web não os dispositivos
- Usuário faz um **requisição a um Servidor Web**, onde o mesmo realiza as requisições/operações com o banco de dados geralmente via rede local, seja em outro computador ou na mesma maquina, muito difícil ambom estarem totalmente separados
![[Desenho;BD;ArquiteturaClienteServidorWEB|640]]
# Modelo de Dados
São conceitos para ==descrever a **estrutura**== de um banco de dados
- **Estrutura:** Tipos de dados, relacionamentos e restrições
- Possui mecanismos de abstração de dados
## Modelos
- Hierárquicos
- Em rede
- Orientado a objeto
- Modelo relacional
- NoSQL
## Conceitos importantes
- **Instância:** Coleção de dados armazenados no ==banco de dados em determinado== momento, como se tirasse uma foto do banco de dados, ou seja, aquele registro naquele momento e uma instância
- **Esquema:** ==Projeto do banco de dados==, incluindo as entidades e os relacionamentos.
- **Linguagem de consulta:** linguagem utilizada para realizar operações no banco de dados, desde extrair, definir e manipular por exemplo podemos utiliza-la para pegar o nome dos funcionários que moram no bairro beija flor na cidade de Osvaldo Cruz 
## Modelo Hierárquico
>[!fail] Desuso
>Estrutura do tipo de **árvore**
![[Desenho;BD;ModeloHierárquico|640]]
>Cada nível da arvore tem correspondência apenas com um nível superior, um elemento pai
## Modelo em rede
> [!fail] Desuso
>Dados organizados em um estrutura de **grafos**
![[Desenho;BD;ModeloEmRede]]
>As entidades tem relacionamento com mais de um entidade pai
## Modelo de Dados
>[!attention] Tem seu uso
Orientado a objeto, baseado na orientação a objetos utilizada na programação
Entidades do mundo real se transformam em classes, com estas classes possuindo propriedades que são suas características, onde a partir das classes  criamos vários objetos com valores atribuídos a suas propriedades
**É utilizado porem menos que o relacional**
![[Desenho;BD;ModeloDeDados|350]]
## Modelo NoSQL
> [!success] Utilizado
> - **Muito utilizado hoje em dia**
> - Banco de dados não relacional, sua vantagem e poder trabalhar com grandes volumes de dados, contem a estrutura **chave valor**, **documentos**, **grafos**  e **pesquisa de dados** 
## Modelo Relacional
>[!success] Muito utilizado
>- **Modelo mais utilizado na atualidade**
>- Os dados são representados em forma de tabelas
>	- Tabela também pode ser chamada de relação
>- Cada coluna possui um domínio que é o tipo de dado daquela coluna
>- Tabelas possuem dados e se relacionam com outras tabelas
>- Desenvolvido a partir de modelos matemáticos como calculo e álgebra relacional
>- Cada linhas é um **registro** ou também chamadas de tuplas
>- Cada coluna representa um valor do registro com seu domínio
>- No modelo relacional as tabelas são relacionadas e não isoladas, ou seja, esta tabela estará relacionada com outras
### Exemplo
| CPF            | Nome         | RA           | RG           |
| -------------- | ------------ | ------------ | ------------ |
| 369.666.356-55 | José Dias    | 006.1.21.256 | 41.354.658-4 |
| 125.569.325-66 | Renata Carla | 006.1.21.088 | 55.569.658-6             |
# Usuários do Banco de Dados
- **Usuário leigo:** Interage com o sistema por meio de uma interface de uma aplicação, sem ter a menor percepção de como os dados estão armazenados e estruturados
- **Projetistas:** Realizam a analise e criam o esquema do banco de dados
- **Desenvolvedores:** Programadores que utilizam o banco de dados para manipular e extrair dados
- **Administradores (DBA):** Gerencia o carregamento dos dados, implementa seguração, backups entre outas funções 
# Níveis de abstração de dados
Criados com a ideia de simplificar a interação do usuário com o sistema, foram criados os níveis de abstração que ocultam a complexidade.
- **Nível físico:** Descreve como os dados são armazenados
- **Nível lógico ou conceitual:** Define a estrutura lógica dos dados
- **Nível da visão:** Descreve como os usuários veem os dados
![[Desenho;BD;AbstraçãoDeDados|350]]
# Gerenciado de armazenamento
É um componente de um sistema de banco de dados que fornece uma interface entre os dados de baixo nível armazenados no banco de dados e os programas aplicativos e consultas submetidas ao sistema
## Componentes
- Gerenciado de autorização e integridade
	- Desrespeito a quais usuários tem acesso a quais dados
- Gerenciador de transação
	- Garante a consistência do banco de dados
- Gerenciador de arquivos
	- Desrespeito a localização física dos dados
- Gerenciador de *buffer*
	- Carregamento de determinadas informação em cache para obter as informação de forma mais rápida
## Estrutura
- **Arquivos de dados:** Arquivos onde os dados são salvos
- **Dicionário de dados:** Metadados para melhorar desempenho
- **Índices:** Mecanismos para acessar os dados de forma mais rápida, funciona como um sumario de um livro