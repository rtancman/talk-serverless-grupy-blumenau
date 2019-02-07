# Criando a estrutura inicial:

```bash

apex init

```

# Alterando estrutura para rodar python

```bash

tree

rm functions/hello/index.js

echo -e "
def handle(event, context):
    return {
        'texto': 'hello world lambda usando apex',
    }
" > functions/hello/main.py


```

# Executando o deploy

```bash

apex deploy

```

# Listando as funcoes

```bash

apex list

```

# Invocando seu lambda

```bash

apex invoke hello

```

# removendo lambda

```bash

apex invoke hello

```