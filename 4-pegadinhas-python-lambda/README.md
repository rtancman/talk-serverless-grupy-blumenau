#criando o arquivo main.py

```bash

echo -e "
import requests
def handle(event, context):
    r = requests.get('https://api.github.com/events')
    return {
        'texto': r.text,
    }
" > main.py

#criando o requirements.txt
echo -e "requests" > requirements.txt

# Rodar o container para instalar as dependências com os comandos do Makefile
make lambda.docker.build lambda.docker.pkgcreate

# zipando
zip -qr dockerhellorequests.zip .

# criar a nossa função via awscli.
aws lambda create-function \
--region us-east-1 \
--handler main.handle \
--runtime python3.7 \
--function-name 'dockerhellorequests' \
--zip-file fileb://./dockerhellorequests.zip \
--role 'arn:aws:iam::032292203206:role/AWSLambdaBasicExecutionRole'

```

#executando o lambda

```bash

aws lambda invoke \
--region us-east-1 \
--function-name 'dockerhellorequests' \
--payload '{}' \
dockerhellorequests.output

cat dockerhellorequests.output

```

# removendo lambda

```bash

aws lambda delete-function \
--region us-east-1 \
--function-name 'dockerhellorequests'

```