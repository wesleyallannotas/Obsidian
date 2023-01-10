---
title: Link Simbolico Windows
author: Wesley Silva
url: 'https://www.todoespacoonline.com/w/2015/04/como-criar-links-simbolicos-no-windows-symlinks'
book:
type: note
completed: true
aliases:
tags: [windows]
description: Como criar link simbolico no windows
---
# Links Simbólicos

```bash
MKLINK [[/d] | [/h] | [/j]] <Link> <Destino>
```

Veja de forma mais detalhada os parâmetros:
-   `/d` – Para um diretório (pasta)
-   `/h` – Para um arquivo qualquer
-   `/j` – Para criar uma junção de diretórios
- `<link>` - Simplesmente o caminho/nome do link simbólico
- `<Destino>` - A pasta ou arquivo original