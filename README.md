# Roteiro para o desenvolvimento da atividade prática do DIO Live Coding do dia 17/11/2021

## Serviços AWS utilizados

- Amazon Cognito
- Amazon DynamoDB
- Amazon API Gateway
- AWS Lambda

## Etapas do desenvolvimento

### Criando uma API REST no Amazon API Gateway

- API Gateway Dashboard -> Create API -> REST API -> Build
- Protocol - REST -> Create new API -> API name [dio_live_api] -> Endpoint Type - Regional -> Create API
- Resources -> Actions -> Create Resource -> Resource Name [Items] -> Create Resource

### No Amazon DynamoDB

- DynamoDB Dashboard -> Tables -> Create table -> Table name [Items] -> Partition key [id] -> Create table

### No AWS Lambda

#### Função para inserir item

- Lambda Dashboard -> Create function -> Name [put_item_function] -> Create function
- Inserir código da função ```put_item_function.js``` disponível na pasta ```/src``` -> Deploy
- Configuration -> Execution role -> Abrir a Role no console do IAM
- IAM -> Roles -> Role criada no passo anterior -> Permissions -> Add inline policy
- Service - DynamoDB -> Manual actions -> add actions -> putItem
- Resources -> Add arn -> Selecionar o arn da tabela criada no DynamoDB -> Add
- Review policy -> Name [lambda_dynamodb_putItem_policy] -> Create policy

### Integrando o API Gateway com o Lambda backend

- API Gateway Dashboard -> Selecionar a API criada -> Resources -> Selecionar o resource criado -> Action -> Create method - POST
- Integration type -> Lambda function -> Use Lambda Proxy Integration -> Lambda function -> Selecionar a função Lambda criada -> Save
- Actions -> Deploy API -> Deployment Stage -> New Stage [dev] -> Deploy

### No POSTMAN

- Add Request -> Method POST -> Copiar o endpoint gerado no API Gateway
- Body -> Raw -> JSON -> Adicionar o seguinte body
```
{
  "id": "003",
  "price": 600
}
```
- Send

### No Amazon Cognito

Devido a alterações na interface do Cognito, precisei seguir o seguinte tutorial, pois estava obtendo erros seguindo o passo-a-passo original:
https://github.com/Jcnok/Bootcamp-Cloud-AWS-DIO/tree/main/desafio-aws-cognito#desafio-de-projeto-adicionando-seguran%C3%A7a-em-apis-na-aws-com-amazon-cognito

Obs1:lembrar de adicionar /login ao Auth URL
Obs2: Não recebi link pelo email ao criar a conta na interface de login e obitve erros ao inserir o código enviado. Porém, ao tentar criar novamente a conta com o mesmo email, indicava que já havia uma conta e então consegui fazer o login. 
Obs3: Não consegui inserir novos itens via postman, nem na fase inicial, tão pouco após a criação do token.
