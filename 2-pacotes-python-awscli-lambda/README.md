# criar a nossa função via awscli.

```bash

mkdir lambda_com_pacotes && cd lambda_com_pacotes

#criando o arquivo main.py
echo -e "
import requests


def handle(event, context):
    r = requests.get('https://api.github.com/events')
    return {
        'texto': r.text,
    }

" > main.py

#criando o requirements.txt
echo -e "requests" >> requirements.txt

#instalando as dependencias para o lambda
pip install -r requirements.txt -t .

# zipando
zip -qr hellorequests.zip .


aws lambda create-function \
  --region us-east-1 \
  --handler main.handle \
  --runtime python3.7 \
  --function-name 'hellorequests' \
  --zip-file fileb://./hellorequests.zip \
  --role 'arn:aws:iam::032292203206:role/AWSLambdaBasicExecutionRole'

```

# invocando um lambda

```bash

aws lambda invoke \
--region us-east-1 \
--function-name 'hellorequests' \
--payload '{}' \
hellorequests.output

cat hellorequests.output

```

# removendo lambda

```bash

aws lambda delete-function \
  --region us-east-1 \
  --function-name 'hellorequests'

```