# LinkKeeper

Esse é o backend da aplicação LinkKeeper - O objetivo dessa aplciação é servir de repositório para todos aqueles links que o usuário deseja salvar, mas que não são tão importantes que mereçam estar na barra do navegador. Além disso, o usuário pode acessar tais links em qualquer lugar, bastando estar logado.

## Endpoints

A API tem um total de 2 endpoints, podendo cadastrar um usuário, realizar um login e criar novos links. 
A url base da API é: https://json-server-base-7f5f.onrender.com

## Criação de Usuário
````````
POST /users - FORMATO DA REQUISIÇÃO
````````
````````
{
  "email": "johndoe@email.com",
  "password": "123456",
  "name": "John Doe",
}
````````
Caso a requisição dê certo, a resposta será da seguinte maneira:
````````
POST /users - FORMATO DA RESPOSTA - STATUS 201
````````
````````
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im5hdGFsaWFAbWFpbC5jb20iLCJpYXQiOjE2ODI2MjMwODcsImV4cCI6MTY4MjYyNjY4Nywic3ViIjoiMiJ9.iB2WB7BjDWcd5PmSZ1C1fZsfNbtJbJi4cY_D_lwWBU",
	"user": {
		"email": "johndoe@mail.com",
		"name": "John Doe",
		"id": 2
	}
}
````````
### POSSÍVEIS ERROS
Caso você acabe enviando algum campo errado, a resposta a esse erro será:
A senha necessita de 6 caracteres.
````
POST /users - FORMATO DA RESPOSTA - STATUS 400
````
````
"Password is too short"
````
## Login
````
POST /login - FORMATO DA REQUISIÇÃO
````
````
{
  "email": "johndoe@email.com",
  "password": "123456"
}
````
Caso a requisição funcione, a resposta será a seguinte:
````
POST /login - FORMATO DA RESPOSTA 
````
````
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImtlbnppbmhvQG1haWwuY29tIiwiaWF0IjoxNjgyNzExMDkzLCJleHAiOjE2ODI3MTQ2OTMsInN1YiI6IjEifQ.QdkfnlXsEVQ6Pm6FzWVmU3Mo1GDeDxDJ_VTxoFDlXqo",
	"user": {
		"email": "johndoe@mail.com",
		"name": "John Doe",
		"id": 1
	}
}
````
### Rotas que necessitam de autorização 
Essas rotas devem ter o token informado no cabeçalho (header) da requisição, no campo "Authorization", dessa maneira:
>Authorization: Bearer {token}
## Autologin
````
GET /users/:userId
````
````
{
	"email": "johndoe@mail.com",
	"password": "$2a$10$dR.mXf7404Po4lU1tFW6hesgFBPHURSNaMEbRLpX3eGNwUnBBL9.q",
	"name": "John Doe",
	"id": 1
}
````
## Links
### Rota para buscar todos os links da API
Não é necessário um corpo para essa requisição 
````
GET /links - FORMATO DA RESPOSTA - STATUS 200
````
````
[
	{
		"id": 1,
		"title": "Link 1",
		"img": "https://kenzie.com.br/_next/image?url=%2Fimages%2Flogo.png&w=256&q=75",
		"comments": "This is a comment",
		"userId": 1
	},
	{
		"title": "Link 1",
		"img": "https://kenzie.com.br/_next/image?url=%2Fimages%2Flogo.png&w=256&q=75",
		"comments": "This is a comment",
		"id": 2,
		"userId": 2
	},
	{
		"title": "Link 3",
		"img": "https://kenzie.com.br/_next/image?url=%2Fimages%2Flogo.png&w=256&q=75",
		"comments": "This is a comment",
		"id": 3
	}
]
````
### Rota para a criação de um novo link
````
POST /links - FORMATO DA REQUISIÇÃO
 ````
````
{
  "title": "Livro 8",
  "img": "https://kenzie.com.br/_next/image?url=%2Fimages%2Flogo.png&w=256&q=75",
  "comments": "This is a comment"
}
````
### Rota para deletar um link
Não é necessário corpo de requisição 
````
DELETE /link/id