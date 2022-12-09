---
title: Note
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: [note, data, python]
description: Como manipular datas no python. 
---
# Biblioteca
Com a biblioteca `DATETIME` podemos facilitar a manipulação de tempo, ela possui uma espécie de submódulos que são as formas como vamos trabalhar

## "Submódulos"
- `DATETIME.DATE` - Desrespeito a data apenas
- `DATETIME.DATETIME` - Desrespeito a data e tempo
- `DATETIME.TIME` - Desrespeito a tempo
- `DATETIME.TIMEDELTA` - Usado quando o objetivo é saber diferença entre períodos de tempo distintos

# Date
- `DATE.CTIME()` - Apresentação da data
- `DATE.TODAY()` - Pega a data atual do sistema
- `DATE.DAY` - Imprimi o dia
- `DATE.MONTH` - Imprimi o mês
- `DATE.YEAR` - Imprimi o ano

# Alterando data
`REPLACE()` - Altera a data já criada
	`replace(month=10)` - Mês 10 é outubro

# Operações com data
```python
from datetime import data

hoje = data.today()
aux = hoje.replace(month=12)
dif = hoje - aux
# Vai gerar um timedelta informando a difereça entre as datas
```