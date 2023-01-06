---
title: Note
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: [bancoDado]
description: Sobre as Linguagens DDL e DML
---
# SQL
> [!summary] Siglas
>- Structured Query Language (SQL)
> 	- Linguagem Estruturada de Consulta
- Usada para criar, manipular e consultar  SGBD relacionais.
- SQL foi desenvolvido no incio dos anos 70 nos laboratórios da IBM
- Embora padronizado pela ANSI e ISO, possui muitas variações e extensões produzidas pelos diferentes fabricantes de sistemas gerenciadores de bancos de dados

# Tipos de comandos SQL
> [!attention] Atenção
> Alguns autores dividem mais.
- **DDL:** Data Definition Language - Linguagem de Definição de Dados
	Comandos que ==interagem com os objetos== do banco
	**Comandos:** CREATE, ALTER e DROP
- **DML:** Data Manipulation Language - Linguagem de Manipulação de Dados
	Comandos que ==interagem com os dados== dentro das tabelas
	**Comandos:** INSERT, DELETE e UPDATE
- **DQL:** Data Query Language - Linguagem de Consulta de dados
	Comandos de consulta
	**Comandos:** SELECT
- **DTL:** Data Transaction Language - Linguagem de Transação de Dados.
	Comandos para controle de transação
	**Comandos:** BEGIN, TRANSACTION, COMMIT e ROLLBACK
- **DCL:** Data Control Language - Linguagem de Controle de Dados
	Controla a parte de seguração do banco de dados
	**Comandos:** GRANT, REVOKE e DENY
	
# Definindo os Dados (DDL)
## Criando o banco de dados
```sql
CREATE DATABASE AULA_EMPRESA;
```

## Criando Tabela
```sql
-- Sintaxe
CREATE TABLE NOME_TABELA(ATRIBUTO TIPO, ATRIBUTO TIPO);
```
>[!example]- Criando Tabelas
>```sql
USE AULA_EMPRESA; -- Seleciona o banco de dados que sera criado as tabelas
>
CREATE TABLE DEPARTAMENTO(
NUMERO INT PRIMARY KEY NOT NULL,
NOME VARCHAR(100) NOT NULL,
DATA_INICIO DATETIME
);
>
CREATE TABLE PROJETO(
NUMERO INT PRIMARY KEY NOT NULL,
NOME VARCHAR(50) NOT NULL,
LOCALIZACAO VARCHAR(50) NOT NULL,
NUMERO_DEPTO INT NOT NULL,
FOREIGN KEY (NUMERO_DEPTO) REFERENCES DEPARTAMENTO(NUMERO)
);
>
CREATE TABLE LOCALIZACOES(
NUMERO_DEPTO INT NOT NULL,
LOCALIZACAO VARCHAR(50) NOT NULL,
FOREIGN KEY (NUMERO_DEPTO) REFERENCES DEPARTAMENTO(NUMERO),
PRIMARY KEY (NUMERO_DEPTO, LOCALIZACAO)
);
>
CREATE TABLE EMPREGADO(
NUMERO_SEGURO_SOCIAL INT PRIMARY KEY NOT NULL,
NOME VARCHAR(150) NOT NULL,
DATA_NASCIMENTO DATE NOT NULL,
SEXO CHAR(1) CHECK(SEXO IN ('F', 'M', 'O')),
RUA VARCHAR(50),
NUMERO VARCHAR(10),
NUMERO_DEPTO INT NOT NULL,
NUMERO_SEGURO_SOCIAL_SUPERVISOR INT,
FOREIGN KEY (NUMERO_DEPTO) REFERENCES DEPARTAMENTO (NUMERO),
FOREIGN KEY (NUMERO_SEGURO_SOCIAL_SUPERVISOR) REFERENCES EMPREGADO(NUMERO_SEGURO_SOCIAL)
);
>
CREATE TABLE HORISTA(
NUMERO_SEGURO_SOCIAL INT PRIMARY KEY NOT NULL,
VALOR_HORA DECIMAL(8,2) NOT NULL,
FOREIGN KEY (NUMERO_SEGURO_SOCIAL) REFERENCES EMPREGADO (NUMERO_SEGURO_SOCIAL)
);
>
CREATE TABLE ASSALARIADO(
NUMERO_SEGURO_SOCIAL INT PRIMARY KEY NOT NULL,
SALARIO DECIMAL(8,2) NOT NULL,
FOREIGN KEY (NUMERO_SEGURO_SOCIAL) REFERENCES EMPREGADO (NUMERO_SEGURO_SOCIAL)
);
>
CREATE TABLE DEPENDENTE(
 CODIGO INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
 NUMERO_SEGURO_SOCIAL INT NOT NULL,
 NOME VARCHAR(150) NOT NULL,
 PARENTESCO VARCHAR(50),
 DATA_NASCIMENTO DATE NOT NULL,
 SEXO CHAR(1) CHECK (SEXO IN ('F', 'M', 'O')),
 FOREIGN KEY (NUMERO_SEGURO_SOCIAL) REFERENCES EMPREGADO (NUMERO_SEGURO_SOCIAL)
);
>
CREATE TABLE PROJETO_EMPREGADO(
NUMERO_SEGURO_SOCIAL INT NOT NULL,
NUMERO_PROJETO INT NOT NULL,
FOREIGN KEY (NUMERO_SEGURO_SOCIAL) REFERENCES EMPREGADO (NUMERO_SEGURO_SOCIAL),
FOREIGN KEY (NUMERO_PROJETO) REFERENCES PROJETO (NUMERO),
PRIMARY KEY (NUMERO_SEGURO_SOCIAL, NUMERO_PROJETO)
);
>```

- **USE:** Seleciona o banco de dados
- **CRETE TABLE:** Cria a tabela 
- **PRIMARY KEY:** Defini como chave primaria (Sintaxe diferente para uma ou varias chaves)
- **NOT NULL:** Não aceita valor nulo
- **FOREIGN KEY (chave) REFERENCES deonde:** A "chave" é uma referencia de uma chave de outra tabela (Repare que primeiro criamos a chave comumente, depois a referenciamos)

> [!NOTE] Dica
> Criamos a coluna sexo com **char(1)**, ou seja, um carácter, porem já t**estamos (check)** se este carácter é F, N ou O

## Alterando Tabela
Clausula (Comando) `ALTER` permite alterar no sentido de ==deletar ou adicionar tabelas==, ou seja, não altera valores nem muda tipo de dado da coluna por exemplo
```sql
-- Adicionado coluna
ALTER TABLE EMPREGADO ADD BAIRRO VARCHAR(50) NOT NULL;

-- Removendo coluna
ALTER TABLE EMPREGADO DROP BAIRRO;

-- Adicionando coluna e criando referencia
ALTER TABLE DEPARTAMENTO 
  ADD NUMERO_SEGURO_SOCIAL_SUPERVISOR INT NOT NULL;
ALTER TABLE DEPARTAMENTO
  ADD FOREIGN KEY (NUMERO_SEGURO_SOCIAL_SUPERVISOR) REFERENCES EMPREGADO(NUMERO_SEGURO_SOCIAL);

-- Alterando coluna para receber valor nulo
ALTER TABLE DEPARTAMENTO CHANGE COLUMN NUMERO_SEGURO_SOCIAL_SUPERVISOR NUMERO_SEGURO_SOCIAL_SUPERVISOR INT NULL; -- Repete o nome duas vezes pois podemos alterar o nome, mantive o mesmo no caso
```

## Apagar
Clausula (Comando) `DROP`  deleta tabelas, existem algumas seguração para não quebrar a estrutura do banco, como por exemplo deletar uma tabela que tem algum ou alguns de seus atributos sendo usado como chave primaria
```sql
DROP TABLE LOCALIZACAO;
```

# Manipulação de Dados (DML)
Saindo da manipulação da estrutura como um todo, para manipular os dados internos da tabela.
> [!attention] Atenção
> Se atente a ==respeitar a restrição da integridade==, ou seja, respeite as regras para aquela dado a ser inserido.

## Inserindo Valores
```sql
INSERT INTO nome_tablea (coluna1, coluna2, coluna3) VALUES (valor1, valor2, valor3);

-- Exemplo real
INSERT INTO PROJETO_EMPREGADO(NUMERO_SEGURO_SOCIAL, NUMERO_PROJETO) VALUES(12, 1);
```
- **Números:** Adicionados Normalmente
- **VarChar() e Char():** Entre aspas
- **Date:** Entre aspas respeitando a regra de data (YYYY-MM-DD)
>[!example]- Adicionando Dados na Tabela
>```sql
-- Inserindo Departamentos
INSERT INTO DEPARTAMENTO(NUMERO, NOME) VALUES(258, 'Tecnologia');
INSERT INTO DEPARTAMENTO(NUMERO, NOME) VALUES(30, 'Gerencia');
INSERT INTO DEPARTAMENTO(NUMERO, NOME) VALUES(31, 'Compras');
INSERT INTO DEPARTAMENTO(NUMERO, NOME) VALUES(32, 'Estoque');
>
-- Inserindo Empregados
INSERT INTO EMPREGADO(NUMERO_SEGURO_SOCIAL, NOME, DATA_NASCIMENTO, SEXO, NUMERO, NUMERO_DEPTO, NUMERO_SEGURO_SOCIAL_SUPERVISOR, BAIRRO, RUA)
VALUES(12, 'José Alcantra', '1990-09-01', 'M', '23', 25, NULL, 'Centro', 'Rua Coqueiro');
INSERT INTO EMPREGADO(NUMERO_SEGURO_SOCIAL, NOME, DATA_NASCIMENTO, SEXO, NUMERO, NUMERO_DEPTO, NUMERO_SEGURO_SOCIAL_SUPERVISOR, BAIRRO, RUA)
VALUES(120, 'Reanto Dias', '1995-05-06', 'M', '222A', 25, 12, 'Centro', 'Rua Botanica');
INSERT INTO EMPREGADO(NUMERO_SEGURO_SOCIAL, NOME, DATA_NASCIMENTO, SEXO, NUMERO, NUMERO_DEPTO, NUMERO_SEGURO_SOCIAL_SUPERVISOR, BAIRRO, RUA)
VALUES(222, 'Isabela Flor', '2020-08-01', 'F', '25', 30, NULL, 'Jd Vila Real', 'Rua 15 de Novembro');
INSERT INTO EMPREGADO(NUMERO_SEGURO_SOCIAL, NOME, DATA_NASCIMENTO, SEXO, NUMERO, NUMERO_DEPTO, NUMERO_SEGURO_SOCIAL_SUPERVISOR, BAIRRO, RUA)
VALUES(227, 'Florisbela Fonseca', '1998-09-25', 'F', '2', 30, 222, 'Centro', 'Av. Antonio Carlos');
INSERT INTO EMPREGADO(NUMERO_SEGURO_SOCIAL, NOME, DATA_NASCIMENTO, SEXO, NUMERO, NUMERO_DEPTO, NUMERO_SEGURO_SOCIAL_SUPERVISOR, BAIRRO, RUA)
VALUES(745, 'Luvas Alves', '2001-08-08', 'M', '98', 32, NULL, 'Jd Nobre', 'Rua 21 de Maio');
INSERT INTO EMPREGADO(NUMERO_SEGURO_SOCIAL, NOME, DATA_NASCIMENTO, SEXO, NUMERO, NUMERO_DEPTO, NUMERO_SEGURO_SOCIAL_SUPERVISOR, BAIRRO, RUA)
VALUES(888, 'Ana Cristina Souza', '2021-06-14', 'F', '88', 31, NULL, 'Jd Morumbi', 'Av. Castilho');
INSERT INTO EMPREGADO(NUMERO_SEGURO_SOCIAL, NOME, DATA_NASCIMENTO, SEXO, NUMERO, NUMERO_DEPTO, NUMERO_SEGURO_SOCIAL_SUPERVISOR, BAIRRO, RUA)
VALUES(848, 'Roberto Carlos', '1988-08-04', 'M', '887', 31, 888, 'Centro', 'Rua 17 de Maio');
INSERT INTO EMPREGADO(NUMERO_SEGURO_SOCIAL, NOME, DATA_NASCIMENTO, SEXO, NUMERO, NUMERO_DEPTO, NUMERO_SEGURO_SOCIAL_SUPERVISOR, BAIRRO, RUA)
VALUES(985, 'Leticia Ramos', '1987-08-09', 'F', '8', 32, 745, 'Alameda Alves', 'Rua das Flores');
>
-- Adicionando Inicio de Cada Supervisor e Sua Data de Inicio
UPDATE DEPARTAMENTO SET DATA_INICIO = '2020-05-01 00:00:00',
 NUMERO_SEGURO_SOCIAL_SUPERVISOR = 12
  WHERE NUMERO = 258;
UPDATE DEPARTAMENTO SET DATA_INICIO = '2019-05-01 00:00:00',
 NUMERO_SEGURO_SOCIAL_SUPERVISOR = 222
WHERE NUMERO = 30;
UPDATE DEPARTAMENTO SET DATA_INICIO = '2020-01-01 00:00:00',
 NUMERO_SEGURO_SOCIAL_SUPERVISOR = 888
WHERE NUMERO = 31;
UPDATE DEPARTAMENTO SET DATA_INICIO = '2020-08-01 00:00:00',
 NUMERO_SEGURO_SOCIAL_SUPERVISOR = 745
WHERE NUMERO = 32;
>
-- Inserindo nas entidades especializadas
INSERT INTO ASSALARIADO(NUMERO_SEGURO_SOCIAL, SALARIO) VALUES(12, 1250.00);
INSERT INTO ASSALARIADO(NUMERO_SEGURO_SOCIAL, SALARIO) VALUES(222, 10000.00);
INSERT INTO ASSALARIADO(NUMERO_SEGURO_SOCIAL, SALARIO) VALUES(745, 1545.65);
INSERT INTO ASSALARIADO(NUMERO_SEGURO_SOCIAL, SALARIO) VALUES(888, 2879.99);
INSERT INTO HORISTA(NUMERO_SEGURO_SOCIAL, VALOR_HORA) VALUES(120, 40.25);
INSERT INTO HORISTA(NUMERO_SEGURO_SOCIAL, VALOR_HORA) VALUES(227, 80.25);
INSERT INTO HORISTA(NUMERO_SEGURO_SOCIAL, VALOR_HORA) VALUES(848, 45.50);
INSERT INTO HORISTA(NUMERO_SEGURO_SOCIAL, VALOR_HORA) VALUES(985, 58.60);
>
-- Inserindo Dependentes (Coluna Codigo se Auto Incrimenta, ignora ela no insert)
INSERT INTO DEPENDENTE(NUMERO_SEGURO_SOCIAL, NOME, PARENTESCO, DATA_NASCIMENTO, SEXO) 
  VALUES(120, 'Lincoln De Nobrega Dias', 'Filho', '2010-02-25', 'M');
INSERT INTO DEPENDENTE(NUMERO_SEGURO_SOCIAL, NOME, PARENTESCO, DATA_NASCIMENTO, SEXO) 
  VALUES(120, 'Rafaela Dias', 'Esposa', '1998-08-09', 'F');
INSERT INTO DEPENDENTE(NUMERO_SEGURO_SOCIAL, NOME, PARENTESCO, DATA_NASCIMENTO, SEXO) 
  VALUES(848, 'Osmar Carlos', 'Filho', '2000-09-25', 'M');
INSERT INTO DEPENDENTE(NUMERO_SEGURO_SOCIAL, NOME, PARENTESCO, DATA_NASCIMENTO, SEXO) 
  VALUES(848, 'Bruna Carla', 'Filha', '2005-05-08', 'F');
INSERT INTO DEPENDENTE(NUMERO_SEGURO_SOCIAL, NOME, PARENTESCO, DATA_NASCIMENTO, SEXO) 
  VALUES(848, 'Tatiana Carla', 'Filha', '2010-08-09', 'F');
>  
-- Inserindo Localização
INSERT INTO LOCALIZACOES(NUMERO_DEPTO, LOCALIZACAO) VALUES(25, 'Bloco 1');
INSERT INTO LOCALIZACOES(NUMERO_DEPTO, LOCALIZACAO) VALUES(25, 'Bloco 2');
INSERT INTO LOCALIZACOES(NUMERO_DEPTO, LOCALIZACAO) VALUES(30, 'Bloco 1');
INSERT INTO LOCALIZACOES(NUMERO_DEPTO, LOCALIZACAO) VALUES(31, 'Bloco 2');
INSERT INTO LOCALIZACOES(NUMERO_DEPTO, LOCALIZACAO) VALUES(32, 'Bloco 3');
>
-- Inserindo Projetos
INSERT INTO PROJETO(NUMERO, NOME, LOCALIZACAO, NUMERO_DEPTO) 
  VALUES(1, 'Projeto A', 'Bloco 1', 25);
INSERT INTO PROJETO(NUMERO, NOME, LOCALIZACAO, NUMERO_DEPTO) 
  VALUES(2, 'Projeto B', 'Bloco 1', 25);
INSERT INTO PROJETO(NUMERO, NOME, LOCALIZACAO, NUMERO_DEPTO) 
  VALUES(3, 'Projeto C', 'Bloco 2', 30);
INSERT INTO PROJETO(NUMERO, NOME, LOCALIZACAO, NUMERO_DEPTO) 
  VALUES(4, 'Projeto D', 'Bloco 2', 31);
INSERT INTO PROJETO(NUMERO, NOME, LOCALIZACAO, NUMERO_DEPTO) 
  VALUES(5, 'Projeto E', 'Bloco 3', 32);
>  
-- Inserindo Projetos nos Empregados
INSERT INTO PROJETO_EMPREGADO(NUMERO_SEGURO_SOCIAL, NUMERO_PROJETO) VALUES(12, 1);
INSERT INTO PROJETO_EMPREGADO(NUMERO_SEGURO_SOCIAL, NUMERO_PROJETO) VALUES(120, 1);
INSERT INTO PROJETO_EMPREGADO(NUMERO_SEGURO_SOCIAL, NUMERO_PROJETO) VALUES(12, 2);
INSERT INTO PROJETO_EMPREGADO(NUMERO_SEGURO_SOCIAL, NUMERO_PROJETO) VALUES(222, 3);
INSERT INTO PROJETO_EMPREGADO(NUMERO_SEGURO_SOCIAL, NUMERO_PROJETO) VALUES(227, 3);
INSERT INTO PROJETO_EMPREGADO(NUMERO_SEGURO_SOCIAL, NUMERO_PROJETO) VALUES(888, 4);
INSERT INTO PROJETO_EMPREGADO(NUMERO_SEGURO_SOCIAL, NUMERO_PROJETO) VALUES(745, 5);
INSERT INTO PROJETO_EMPREGADO(NUMERO_SEGURO_SOCIAL, NUMERO_PROJETO) VALUES(985, 5);
>```

## Alterando Dados
Altera os valores do registro da tabela.
>[!attention] Ateção
>Se não utilizar o `WHERE` ira alterar todos os valores da tabela.
>```sql
UPDATE nome_table SET coluna1 = valor1;
>
-- Exemplo de caso real.
UPDATE DEPARTAMENTO SET DATAINCIO = '2020-02-01',
  NUMERO_SEGURO_SOCIAL_SUPERVISOR = 8673
  WHERE NUMERO = 25;
>```

## Deletando Valores
Deletando um registro da tabela.
>[!attention] Atenção
>Sem o uso do clausula (comando) `WHERE`, deletara todos o registros da tabela
>```sql
DELETE FROM NOME_TABELA WHERE CONDICAO;
>
-- Exemplo de uso
DELETE FROM EMPREGADO WHERE NUMERO_SEGURO_SOCIAL = 2234;
>```

# Consulta (DQL)
Comandos que lidam com a consulta de dados (Extração de dados) do Banco de Dados
## Sintaxe
```SQL
-- Simples
SELECT * FROM NOME_TABLEA;

-- Teste (WHERE)
SELECT * FROM EMPREGADO WHERE NUMERO_SEGURO_SOCIAL = NULL

-- Colunas Especificas
SELECT CODIGO, NOME FROM DEPENDENTE;

-- Coluna e Teste
SELECT CODIGO, NOME FROM DEPENDETE WHERE CODIGO = 5;

-- Ordenando por determina coluna
SELECT CODIGO, NOME FROM DEPENDENTE ORDER BY CODIGO;
```
Operações realizadas com o `SELECT` só possui efeito visual, assim ==não ocasionando mudação nos dados armazenados no Banco de Dados.==
- `SELECT` dentro de `SELECT` é uma **subquery**

## Renomeando Colunas
```sql
SELECT NOME as 'Nome', NUMERO_SEGURO_SOCIAL as 'Seguro Social' FROM EMPREGADO;
```

## Ordenação
Usamos o clausula (comando) `ORDER BY`
- Por padrão a ordenação ocorre de forma crescente `ASC`
- Ordenar de forma decrescente `DESC`
```sql
-- Ordenando pela coluna nome de forma decrescente
SELECT *
FROM EMPREGADO
ORDER BY NOME DESC

-- Cadeia de ordenação
SELECT *
FROM EMPREGADO
ORDER BY SEXO, NOME; -- Primerio ordena pelo sexo, depois pelo nome.

-- Possivel misturar o tipo de ordenção
SELECT * 
FROM EMPREGADO
ORDER BY SEXO DESC, NOME ASC; -- Não precisava do ASC, pois, é padrão

-- Exemplos
SELECT NOME AS 'Nome', NUMERO_SEGURO_SOCIAL AS 'Seguro Social', SEXO AS 'Sexo', DATA_NASCIMENTO AS 'Data de Nascimento'
FROM EMPREGADO
WHERE NUMERO_DEPTO = 30 OR NUMERO_DEPTO = 25
ORDER BY SEXO DESC, NOME ASC;
```

## Operadores
SQL disponibiliza diversos operadores para que possamos refinar nossas comandos
- Agrupamento - Através dos parênteses `( )` podemos agrupar qualquer operadores.
- Matemáticos - Adição `+`, Subtração `-`, Multiplicação (`*`), Divisão (`/`), Modulo (`%`)
- Logico - E (`AND`), OU (`OR`), Não (`NOT`)
- Comparação - Maior (`>`), Menor (`<`), Maior Igual (`>=`), Menor Igual (`<=`), Diferente (`<>`, `!=`), Igual (=)
- `DISTINCT` - Adicionando esse operador antes do nome da coluna, pegas valores que não se repetem apenas
- `IS NULL` - É nulo, ou seja, não possui valor.
	- Vale lembrar que o `NOT` pode ser utilizar para obter os não nulos
- `IN` - O valor da coluna a ser comparada, precisa se encontrar no  valor dentro dos parênteses, seja `SELECT` ou lista de valores, operador `IN` é amplamente utilizado em Python.
	- Vale lembrar que o `NOT` também pode ser utilizado para obter valor contrario.
- `LIKE` - Comparador de texto, utilizamos o `%` para informar que possui texto para aquela direção
	- `G%` - Começa com G
	- `A%` - Termina com G
	- `%T%` -  T no meio do texto
- `BETWEEN` - Pega dois valores e filtra entre o intervalo entre eles, muito utilizado para datas
	- `BETWEEN '2000-01-01' AND '2020-12-31'` - Pegara as datas entre as duas, **Cada SGBD utiliza um formato para data**
 - `EXISTS` - ==Verifica a existência==, Precisa existir, mas não unicamente um atribuo e sim um conjunto de linha (tuplas)
	- Compara existência de tuplas
```sql
SELECT *
FROM EMPREGADO
WHERE (SEXO = 'F' AND NUMERO_DEPTO = 30)
OR (SEXO = 'M' OR SEXO IS NULL);

-- Operador LIKE
SELECT * FROM EMPREGADO
WHERE BAIRRO = 'Centro' AND RUA LIKE 'Rua%'; -- Começa com rua e depois tem qualquer coisa

-- Operador BETWEEN intervalo
SELECT * FROM EMPREGADO
WHERE DATA_NASCIMENTO BETWEEN '2000-01-01' AND '2020-12-31';

-- Para comparar com nulos se usa o IS
SELECT * FROM EMPREGADO WHERE NUMERO_SEGURO_SOCIAL_SUPERVISOR IS NULL;
SELECT * FROM EMPREGADO WHERE NUMERO_SEGURO_SOCIAL_SUPERVISOR IS NOT NULL;

-- Elimina os iguais
SELECT DISTINCT BAIRRO FROM EMPREGADO;

-- Operador `in`
SELECT NUMERO_SEGURO_SOCIAL, NOME, DATA_NASCIMENTO
FROM EMPREGADO
WHERE NUMERO_SEGURO_SOCIAL IN (SELECT NUMERO_SEGURO_SOCIAL FROM ASSALARIADO); 
-- Ira filtranr a partir se o numero desta tabela se encontra na outra

-- Lista de valores
SELECT ID_FUNCIONARIO
  FROM FUNCIONARIOS
 WHERE ID_FUNCIONARIO IN (2, 5, 25);

-- Comando/Operador `exists`
SELECT * 
FROM DEPARTAMENTO DEPTO
WHERE EXISTS(SELECT  *
             FROM PROJETO
             WHERE NUMERO_DEPTO = DEPTO.NUMERO);
             
SELECT * FROM EMPREGADO EMP
WHERE EXISTS(SELECT * FROM PROJETO_EMPREGADO
             WHERE NUMERO_SEGURO_SOCIAL = EMP.NUMERO_SEGURO_SOCIAL);
```

## Comando `UNION`
- União `UNION` a quantidade e o tipo das colunas precisão ser as mesmas
	- Order precisar vir no final.
```sql
-- União
SELECT NOME, DATA_NASCIMENTO FROM EMPREGADO
UNION
SELECT NOME, DATA_NASCIMENTO FROM DEPENDENTE
ORDER BY 1; -- Ordenar pela primeira coluna (no caso nome)
```

## Função Agregada
Utilizamos para fazer cálculos por exemplo.
- `COUNT()` - Realiza uma contagem
- `MIN()` - Menor
- `MAX()` - Maior
- `AVG()` - Media
- `SUM()` - Soma
Realiza uma contagem.
```sql
SELECT COUNT(*) FROM EMPREAGDO; -- Contara todas as colunas da tabela empregado
SELECT MIN(DATA_NASCIMENTO) FROM EMPREGADO;
SELECT MAX(DATA_NASCIMENTO) FROM EMPREGADO;
SELECT COUNT(NUMERO_SEGURO_SOCIAL) FROM ASSALARIADO;
SELECT AVG(SALARIO) FROM ASSALARIADO;
SELECT SUM(SALARIO) FROM ASSALARIADO;
```

## Agrupamento
Comando `GROUP BY`, normalmente é utilizado junto com as funções agregadas
- `ORDER BY` vem depois do `GROUP BY`
```sql
SELECT NUMERO_DEPTO, COUNT(*)
FROM EMPREGADO
GROUP BY NUMERO_DEPTO;

SELECT NUMERO_DEPTO as 'Departamento', COUNT(*) as 'Funcionarios'
FROM EMPREGADO
GROUP BY NUMERO_DEPTO;

SELECT NUMERO_SEGURO_SOCIAL, COUNT(*) AS 'Quantidade'
FROM DEPENDENTE
GROUP BY NUMERO_SEGURO_SOCIAL
ORDER BY Quantidade;

SELECT NUMERO_DEPTO, COUNT(SEXO) AS 'QUANTIDADE_MULHERES'
FROM EMPREGADO
WHERE SEXO = 'F'
GROUP BY NUMERO_DEPTO
ORDER BY QUANTIDADE_MULHERES DESC;
```

## Filtragem nas Funções Agregadas
Comando `HAVING`, depois do `GROUP BY`  e antes do `ORDER BY`.
Funciona como uma clausula(comando) `WHERE` porem apenas para as funções agregadas.
Ou seja, a partir do que a função retornar.
```sql
SELECT NUMERO_SEGURO_SOCIAL, COUNT(*)
FROM DEPENDENTE
GROUP BY NUMERO_SEGURO_SOCIAL
HAVING COUNT(*) > 2
ORDER BY NUMERO_SEGURO_SOCIAL DESC;
```

## Apelidando Tabelas
Faz mais sentido usar com o `JOIN`, pois, iremos nos referenciar a mais de uma tabela, para apelidar uma tabela podemos ou não usar o `AS`
```sql
SELECT EMP.COD, EMP.NOME, EMP.CPF, A.SALARIO
FROM EMPREGADO EMP
INNER JOIN ASSALARIADO A
ON EMP.COD = A.COD_EMPREGADO;

-- Utilizando AS
SELECT EMP.COD, EMP.NOME, EMP.CPF, A.SALARIO
FROM EMPREGADO AS EMP
INNER JOIN ASSALARIADO AS A
ON EMP.COD = A.COD_EMPREGADO;
```

## Junção de Tabelas
Possuímos alguns tipos de junções sendo elas.
![[Desenho_SQL_Joins|650]]
- `INNER JOIN` - **Mais Utilizado**, junção interna, junta as duas tabelas, ou seja, seus atributos baseado em uma comparação que vai ser especificada apos o `ON`, possível juntar varias tabelas, e também é possível, adicionar mais de uma comparação usando operado `AND`
>[!example]- Exemplo
> `AS` é opcional para dar apelido a tabela/relação.
>```sql
SELECT E.NUMERO_SEGURO_SOCIAL, E.NOME, COUNT(D.NOME) AS QTD_DEPENDENTE, DP.NOME 
FROM EMPREGADO AS E
INNER JOIN DEPENDENTE AS D
ON E.NUMERO_SEGURO_SOCIAL = D.NUMERO_SEGURO_SOCIAL
INNER JOIN DEPARTAMENTO AS DP
ON E.NUMERO_DEPTO = DP.NUMERO
GROUP BY E.NUMERO_SEGURO_SOCIAL;
>```
- `LEFT JOIN` - Junção à esquerda, todas as direitos mas quando tiver os da direita retornar também, caso não tenho, retorna `NULL`
>[!example]- Exemplo
>```sql
>SELECT E.NUMERO_SEGURO_SOCIAL AS 'SEGURO', E.NOME AS 'EMPREAGO',
D.NOME AS 'DEPENDENTE', DP.NOME AS 'DEPARTAMENTO'
FROM EMPREGADO AS E
LEFT JOIN DEPENDENTE AS D
ON E.NUMERO_SEGURO_SOCIAL = D.NUMERO_SEGURO_SOCIAL
INNER JOIN DEPARTAMENTO AS DP
ON E.NUMERO_DEPTO = DP.NUMERO;
>```
- `RIGHT JOIN` - Junção à direita, funciona como o `LEFT JOIN` porem para a outra direção
- `CROSS JOIN` -  Cruza todas as linhas de uma relação(tabela) com a outra relação(tabela), independente de serem ou não relacionados.
>[!example]- Exemplo
>```sql
>SELECT * 
FROM EMPREGADO
CROSS JOIN DEPENDENTE
-- Para cada empregado, vai fazer um join, com todos os dependentes, ou seja, retorna um numero exorbitante de linhas, basicamente, quantidade de empregados vezes quantidade de dependentes.
>```
- `FULL OUTER JOIN` - Faz uma junção de todos os Joins (Menos o `CROSS JOIN`), em MySQL não existe, seria necessário utilizar o `UNION`

# View
Armazena comandos `SELECT`, assim não sendo necessário ficar reescrevendo o SQL, muito útil quando escrevemos uma aplicação que utiliza muito de determinado extração de dados.
```SQL
CREATE VIEW VW_EMPREAGO_ASSALARIADO AS 
SELECT E.NUMERO_SEGURO_SOCIAL, E.DATA_NASCIMENTO, E.SEXO, A.SALARIO 
FROM EMPREGADO E
INNER JOIN ASSALARIADO A
ON E.NUMERO_SEGURO_SOCIAL = A.NUMERO_SEGURO_SOCIAL;
```
Fica contido os dados e são atualizadas automaticamente com o decorrer da manipulação de dados, ou seja, uma `VIEW` não é estática,  pois, na verdade ela guarda o `SELECT` não os dados.\

## Utilizar uma View
Basta utilizarmos no lugar da referencia a uma tabela, ou seja, no `FROM`
```sql
SELECT * FROM VW_EMPREAGO_ASSALARIADO;
```
Funciona como uma tabela, podemos usar todas as ferramentas disponíveis, como `WHERE` os `JOIN` entre outro.
```sql
SELECT * FROM VW_EMPREAGO_ASSALARIADO WHERE SALARIO > 2000;
```

# Procedures (Stored Procedures)
Uma função, ou melhor, um procedimento a ser executado no banco de dados (Precisa ser chamado), por exemplos varias operações executados a pois uma vende, em vez de fazer na mão, criamos um procedimento.
- Em um Stored Procedure ==pode-se ter estruturas de controle e decisão==, típicas das linguagens de programação.
- ==Sintaxe difere muito entre SGBDs diferentes==
- Interessante usar ==nome dos parâmetros diferentes dos atributos das tabelas para não ocorrer confusão==
- `IN`  - Parâmetros de entrada
- `OUT` - Parâmetros de saída
- `INTO` - Para atribuir o valor à uma variável
```mysql
DELIMITER $ -- Informamos o `$` como delimitador da PROCEDURE
CREATE PROCEDURE nome_procedimento (parâmetros)
BEGIN
/*CORPO DO PROCEDIMENTO*/
END $
DELIMITER ; -- Voltamos ao delimitador padrão

-- Exemplo
DELIMITER $
CREATE PROCEDURE spAjustaSalario(IN percentual DECIMAL(8,2), numDepto INT, OUT qtdFuncionarios INT)
BEGIN
  -- Contamos os funcionaros através dos filtros do `WHERE` e jogamoes da variável de saida `qtdFuncionarios`
  SELECT COUNT(*) INTO qtdFuncionarios 
  FROM EMPREGADO 
  WHERE NUMERO_DEPTO = numDepto AND NUMERO_SEGURO_SOCIAL IN (SELECT NUMERO_SEGURO_SOCIAL FROM ASSALARIADO);

  -- Atualizamos o valor do salario dos funcionarios através do percentual passado pelo parâmetros de entrada
  UPDATE ASSALARIADO 
  SET SALARIO = SALARIO = (SALARIO * percentual / 100)
  WHERE NUMERO_SEGURO_SOCIAL IN (SELECT NUMERO_SEGURO_SOCIAL FROM EMPREGADO WHERE NUMERO_DEPTO = numDepto);
END $
DELIMITER ;
```
MySQL Workbench possui um bloquei de segurança, necessário remover caso de erro.
```mysql
SET SQL_SAFE_UPDATES=0;
```

### Excluir `PROCEDURE`
```mysql
DROP PROCEDURE nome_procedure;
```

### Utilizando `PROCEDURE`
Os parâmetros criados precisam ser passados na mesma ordem que foram declarados.
- **Entrada** - Pode ser passado o valor direto
- **Saída** - Precisa de uma variável
```mysql
 CALL nome_procedure (parametros);
 
-- Exemplo de uso
CALL spAjusteSalario (10, 25, @qtdFuncionarios);
SELECT @qtdFuncionarios; -- Exibir
```

### Declarando Variáveis
```mysql
DECLARE nome varchar(150);
```

### Estruturas
Dentro de `PROCEDURES` podemos utilizar estruturas, como em uma linguagem de programação por exemplos, laços de repetição.

# Trigger
Também chamado de gatilhos, são procedimentos que são executas através de um gatilho/evento, assim obrigatoriamente, uma Trigger esta associada a uma tabela.
- ==Sintaxe do MySQL, pode variar bastante entre os diferentes tipos de SGBDs==
- **Momento** - Pois pode ocorrer antes ou depois de um determinado evento
	- `BEFORE` ou `AFTER`
- `FOR EACH ROW` - Para cada linha
- Quando trabalhos com Triggers, conseguimos recuperar valor da tabela que ela esta relacionada, conseguindo recuperar **novos valores** e os **antigos valores**
	- `UPDATE` - Possui antigos e novos valores
	- `INSERT` - Apenas novos valores
	- `DELETE` - Apenas antigos valores
	- `NEW` para novos, `OLD` para antigos
- **Eventos** - Operação de `UPDATE`, `INSERT` e `DELETE`
- Cuidado com as implantações de Trigger, pois, Trigger não vê nível de permissão, assim você pode criar uma brecha
```mysql
DELIMITER $
CREATE TRIGGER nome momento evento
ON tabela
FOR EACH ROW
BEGIN
/*CORPO DO CÓDIGO*/
END $
DELIMITER ;
```
>[!example]- Exemplo de Uso de Trigger
>Vamos criar uma tabela para armazenar um histórico de alteração salarial,ou seja, sera uma trigger que se origina na tabela ASSALARIADO e que inseri valores na tabela ASSALARIADO_HISTORICO
>```sql
>-- Criando Tabela
>CREATE TABLE ASSALARIADO_HISTORICO(CODIGO INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
NUMERO_SEGURO_SOCIAL INT NOT NULL,
SALARIO_ANTERIOR DECIMAL(8,2) NOT NULL,
DATA DATETIME NOT NULL,
SALARIO_NOVO DECIMAL(8,2) NOT NULL,
FOREIGN KEY (NUMERO_SEGURO_SOCIAL) REFERENCES EMPREGADO(NUMERO_SEGURO_SOCIAL));
>-- Criando Trigger
>DELIMITER $
CREATE TRIGGER tgArmazenaSalario AFTER UPDATE
ON ASSALARIADO
FOR EACH ROW
BEGIN
 INSERT INTO ASSALARIADO_HISTORICO(NUMERO_SEGURO_SOCIAL, SALARIO_ANTERIOS, DATA, SALARIO_NOVO) 
 VALUES(new.NUMERO_SEGURO_SOCIAL, OLD.SALARIO, CURDATE(), NEW.SALARIO);
END $
DELIMITER ;
>```

# Transação
Unidade lógica onde **todas** as instruções nela contida, devem ser executadas, essas instruções são uma ou varias operações (Inserção, Exclusão, Alteração ou Recuperação), ==não precisa necessariamente ser na mesma tabela==, todos precisão ocorrer sem erros
- **Iniciar** - `start transaction`
- **Finalizar** - `commit` (Sucesso) ou `rollback` (Falha)

## Exemplos de Transações
- Transferência bancária
- Transferência de fundos
- Reserva de passagem
- Venda ao consumidor
- Comércio entre empresas
- Alocação de recursos
- Controle de estoque
```mysql
-- Exemplo: Aplicação Financeira
Begin Transaction Aplicação
Update Conta Set Saldo = Saldo - @valor
Where NumConta = @num
Update Aplic Set Saldo = Saldo + @valor
Where NumConta = @num and Tipo = @tipo
Commit Transaction Aplicação
```
>[!example]- Exemplo de Transação
>```sql
>-- Criando uma trasação
-- Vamos inserir daods no empregado e no assalariado e queremos garantis a consistência
DELIMITER $
CREATE PROCEDURE sp_inserirEmpregadoAssalariado(IN NUMERO_SEGURO_SOCIAL INT,
IN NOME VARCHAR(150), IN DATA_NASCIMENTO DATE, IN SEXO CHAR(1), IN NUMERO VARCHAR(10), 
IN NUMERO_DEPTO INT, IN NUMERO_SEGURO_SOCIAL_SUPERVISOR INT, IN BAIRRO VARCHAR(150), 
IN RUA VARCHAR(150), IN SALARIO DECIMAL(10,2))
BEGIN
DECLARE EXIT HANDLER FOR SQLEXCEPTION
BEGIN
ROLLBACK;
END; -- Este inicio informa que caso ocorra um erro, realize um rollback
START TRANSACTION;
INSERT INTO EMPREAGDO(NUMERO_SEGURO_SOCIAL, NOME, DATA_NASCIMENTO, 
SEXO, NUMERO_DEPTO, NUMERO_SEGURO_SOCIAL_SUPERVISOR, BAIRRO, RUA, NUMERO) 
VALUES(NUMERO_SEGURO_SOCIAL, NOME, DATA_NASCIMENTO, SEXO, NUMERO_DEPTO, 
NUMERO_SEGURO_SOCIAL_SUPERVISOR, BAIRRO, RUA, NUMERO);
INSERT INTO ASSALARIADO(NUMERO_SEGURO_SOCIAL, SALARIO) VALUES (NUMERO_SEGURO_SOCIAL, SALARIO);
COMMIT;
END $ 
DELIMITER ;
>```
Falamos que transação e uma unidade lógica e tão importante, pois, evita erros, pois obriga a execução em sua totalidade, ==primordial para manter a consistência==

## Propriedades ACID
ACID (Atomicidade, Consistência, Isolamento e Durabilidade), toda transação deve garantir essas propriedades
- **Atomicidade** - Garante que as operações serão atômicas (indivisíveis) ou ocorreram em sua totalidade ou não ocorreram
- **Consistência** - Garante que um banco de dados passará de uma forma consistente para outra forma consistente, não podendo alterar para um banco inconsistência
- **Isolamento** - Garante que a transação não será interferida por nenhuma outra transação concorrente
- **Durabilidade** - Garante que o que foi salvo, não será mais perdido

## Estados da Transação
Estados possíveis ao final de uma transação
- **Efetivada (commit)** - Transação ocorrida com sucesso
- **Abortada** - Transação não foi concluída devido a falha, implica em desfazer todas as alterações (rollback)
![[Desenho_BD_Transação|650]]

## Sistema de controle de concorrência
Transações podem ser executadas:
- **Sequencialmente** - Uma apos a outra
- **Concorrentemente** - Partes das transações podem ser processadas em paralelo
Concorrência entre transações é ==necessária para melhor desempenho==, melhora o *throughput* (Número de transações por quantidade de tempo) e utilização dos recursos, ocasionando em um ==tempo de espera reduzido==, porem e mais difícil mantes a consistência do banco de dados, podem ocorrer "Leitura ou Escrita Suja", o ideal é criar ==escalas para que possa garantir a consistência==, casso ocorra um erro é necessário o *rollback* em cascata, desfazendo as mudanças, a recurção de estado é dificultada quando há concorrência entre transações
### Serialização
Uma escala que é concorrente é o ideal, pois, possui mais desempenho no banco de dados, porem precisa manter a concorrência, ou seja, produzir o mesmo resultado de uma transação sequencial, caso satisfaça estes requisitos podemos enter como uma escala serializavel, para isso consideraremos as operações de leitura e escrita
### Bloqueios
Para garantir a  seriação, ou seja, leitura e a escrita correta em operações concorrentes, as vezes se torna necessário os bloqueios, funciona na ideia que ==uma operação pode bloquear determinado dado que esta utilização, assim outra operação que utiliza este dado só poderá ser iniciada apos a liberação do dado==, existem dois tipos de bloquei sobre um dado:
- **Compartilhado (S)** - Pode ler, mas não pode escrever
- **Exclusivo (X)** - Pode ler e escrever, obrigado o outro independente da operação com o dado ter que esperar
### Impasse (DeadLock)
Ocorre quando as transações ficam paradas esperando um dado que esta bloqueado por outra, assim  uma esperando pelo dado da outra, ocorrendo um travamento, isso e chamado de impasse ou *deadlock*, quando ocorre é necessário um rollback inteiro ou parcial (ate o ponto que obteve um bloqueio cujo liberação resolve o impasse)
Para evitar o impasse os SGBD utilizando de alguns mecanismos:
- Prevenção de impasse
- Baseados em tempo limite
- Detecção e recuperação de impasse
### Sistema de Recuperação de Falhas
- Falhas de transação:
	- Erro lógico (Entrada defeituosa, dados não encontrados, etc)
	- Erro do sistema (impasse)
- Falha do sistema, perda de dados do armazenamento volátil, provocadas por hardware ou software
- Falha no disco
>[!note] Tipos de Armazenamento
>- **Volátil** - Memória principal, cache
>- **Não Volátil** - Discos e fitas magnéticas
>- **Estável** - Replicar a informação em vários meios não voláteis (Espelhamento)

Existem sistemas de recuperação que ==devem garantir as propriedades ACID==
==A transação é concluído sendo efetivada ou abortada==
*Rollback* consiste em desfazer as operações voltando ao estado estável anterior, o mesmo ==ocorre com base nos *logs*== que mantem o registro das operações no banco de dados, onde o mesmo considerado uma transação efetiva aquele que o SGBD encontre o inicio e o fim (*commit*) da mesmo, caso não encontra realiza o *rollback*, porem para ler o *log* inteiro é muito demorado, assim de forma inteligente o ==banco de dados cria *checkpoints* periodicamente==, que são gravados no disco os dados em memória e os registros de *log*, sendo inserido um registro `<chackpoint>` no *log*, assim quando ocorre um erro, o ==*log* é lido do fim ao inicio ate encontrar um *checkpoint*==, e a recuperação é realizada a partir deste ponto, pois, de um *checkpoint* para trás não faz sentido ler, pois, as operações anteriores já foram validades e registradas.
### Backup
Manter uma copia da base de dado casso ocorra eventuais problemas, preferencialmente ao menos diário, manter em locais distintos (Não faz sentido fazer backup no mesmo dispositivo), muito interessante manter um espelhamento do disco também assim mantendo uma redundância de dados (Caso ocorra o problema em um o outro assume) algo que é muito importante para uma base de dados
- Para fazer o backup basta ir em **Administration** > **Data Export**
	- Podemos exportar em um único arquivo ou em vários separados em diretórios
	- E caso queira exportar a criação das tabelas, marcar a checkbox
- Para Importar o backup basta ir em **Administration** > **Data Import**
	- Selecionar a opção condizente, ou seja, de um ou vários arquivos
	- Selecionar uma  DataBase ou criar um novo
# Controle de Dados (DCL)
Quais alterações podem ser executadas sobre qual objeto por determinado usuário, restrições importantes para implementar seguração no banco de dados.
Por exemplo funcionários de estoque não deve ter acesso a os salários dos funcionários.
- Aba **Administration** no canto esquerdo > **Users and Privileges** > **Add Account**
## Concedendo Permissão
Usamos o comando `GRANT`
```SQL
-- Sintaxe
GRANT DIREITOS ON OBJETOS TO USUARIO;
-- Permissão de usar select (Pesquisa)
GRANT SELECT ON EMPREGADO TO usuario1;
-- Permissões
GRANT SELECT, UPDATE, DELETE, INSERT on EMPREGADO TO usuario2;
```
## Revogando Permissões
```sql
-- Sintaxe
REVOKE DIRETOS ON OBJETOS FROM USUARIO;
-- Revogando usuario1
REVOKE SELECT ON EMPREGADO FROM usuario1;
-- Revogando usuario2
REVOKE DELETE ON EMPREGADO FROM usuario2;
```

# Comandos Interessantes
- `CURDATE()` - Pega data atual
- **Mostras Todas Tabelas:** `SHOW TABLES`