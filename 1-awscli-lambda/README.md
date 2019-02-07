# criar a nossa função via awscli.

```bash

echo -e "
def handler(event, context):
    return {
        'texto': 'hello world lambda usando awscli',
    }
" > main.py

zip -qr awsclicreatelambda.zip main.py

aws lambda create-function \
  --region us-east-1 \
  --handler main.handler \
  --runtime python3.7 \
  --function-name 'awscli-create-lambda' \
  --zip-file fileb://./awsclicreatelambda.zip \
  --role 'arn:aws:iam::032292203206:role/AWSLambdaBasicExecutionRole'

```

##Fique ligado!
- arquivo zip: Seu código lambda precisa ter menos de 10mb caso contrário precisa subir o seu codigo zip para o S3
- role: Precisamos passar a ARN da role de execução

# listar nossos lambdas via awscli.

```bash

aws lambda list-functions

```

# atualizar nossos lambdas via awscli.

```bash

aws lambda update-function-code \
  --region us-east-1 \
  --function-name 'awscli-create-lambda' \
  --zip-file fileb://./awsclicreatelambda.zip

```

# invocar nossos lambdas via awscli.

```bash

aws lambda invoke \
  --region us-east-1 \
  --function-name 'awscli-create-lambda' \
  --payload '{}' \
  awsclicreatelambda.output

```

# deletar nossos lambdas via awscli.

```bash

aws lambda delete-function \
  --region us-east-1 \
  --function-name 'awscli-create-lambda'

```