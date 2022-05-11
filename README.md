O objetivo dessa aplicação é conseguir criar, listar usuarios e adicionar receitas entre doces e salgados.

json-server-base
Esse é o repositório com a base de JSON-Server + JSON-Server-Auth já configurada, feita para ser usada no desenvolvimento das API's.

Endpoints
Assim como a documentação do JSON-Server-Auth traz (https://www.npmjs.com/package/json-server-auth), existem 5 endpoints que podem ser utilizados. A url base da API é :

Rotas que não precisam de autenticação
Listando usuários
GET /users - FORMATO DA RESPOSTA - STATUS 200

{
"email": "kenzinho@mail.com",
"password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOJnsZU7FO",
"name": "Kenzinho",
"age": 38,
"id": 1
},
{
"email": "suelly@mail.com",
"password": "$2a$10$ekLf7oGhH66iqn2IN1O4ouK4w9gRoySjM6r3J7BoAOrJ1nqi31l5W",
"name": "suelly",
"age": 40,
"id": 2
}
GET /receitas - FORMATO DA RESPOSTA - STATUS 200

{ "type": "sweet", "title": "brgadeiro", "level": "easy" }, { "type": "salty", "title": "pastel", "level": "easy" }

Criação de usuário
POST /register - FORMATO DA RESPOSTA - STATUS 201

Cadastrar o usuário na lista de "Users", sendo que os campos obrigatórios são os de email e password. Você pode ficar a vontade para adicionar qualquer outra propriedade no corpo do cadastro dos usuários.

{ "email": "suelly3@mail.com", "password": "123456", "name": "suelly3", "age": 40, "ocupação": "estudante"

}

POST /login - FORMATO DA RESPOSTA - STATUS 200 Usado para realizar login com um dos usuários cadastrados na lista de "Users"

{ "email": "suelly1@mail.com", "password": "123456" }

Rotas que necessitam de autorização
POST /receitas - FORMATO DA RESPOSTA - STATUS 201

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

Authorization: Bearer {token}

Após o usuário estar logado, ele deve conseguir cadastrar os tipos de receitas desde que o usuário seja o proprietário do recurso se esse recurso tiver uma propriedade userId que corresponda à sua propriedade id.

{

"type": "salty",
"title": "salgadinho",
"level": "easy", "userId": 1

} { "type": "sweet", "title": "brgadeiro", "level": "easy", "userId": 2 }
