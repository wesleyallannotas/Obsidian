# Plano de Estudo
```dataview
TASK
FROM "01 - Notes/Code/Planejamento"
SORT file.name ASC
```

# Livros 
```dataview
TABLE description as Descrição
FROM #book
WHERE !completed
SORT file.name ASC
```

# Artigos
```dataview
TABLE description as Descrição
FROM #article
WHERE !completed
SORT file.name ASC
```

#  Notas
```dataview
TABLE description as Descrição
WHERE !completed and type = note
SORT file.name ASC
```