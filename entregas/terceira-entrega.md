# Primeira Entrega

## Descrição

Durante essa entrega você terá que desenvolver as rotas e telas referentes as funcionalidades de gerenciamento de objetos e listagem de objetos por local.

## Requisitos Funcionais

Os requisitos funcionais que estão relacionados com essa entrega são:

- **RAP02 - Gerenciar os objetos do local**: O sistema deve permitir que o administrador do local realize o cadastro de novos objetos para serem listados na plataforma, além de permitir a alteração dos dados de um objeto existente e sua exclusão.

## RAP02 - Gerenciar os objetos do local

Abaixo você encontrará todas as informações do quê e como deve ser desenvolvido no back-end e no front-end para o caso de uso RAP02.

## Back-end

### Rotas

| Rota                    | Verbo HTTP | Descrição                                                                         |
|-------------------------|------------|-----------------------------------------------------------------------------------|
| /api/objetos            | GET        | Rota responsável por listar os objetos cadastrados para o local do usuário logado |
| /api/objetos            | POST       | Rota responsável por cadastrar um objeto o local do usuário logado                |
| /api/objetos/{objetoId} | GET        | Rota responsável por exibir os dados de um objeto                                 |
| /api/objetos/{objetoId} | PUT        | Rota responsável por alterar dados de um objeto                                   |
| /api/objetos/{objetoId} | DELETE     | Rota responsável por excluir um objeto                                            |

### Rota GET /api/objetos

**Dados da requisição**

Não se aplica

**Dados da resposta**

| Campo         | Tipo     | Exemplo                                                                    |
|---------------|----------|----------------------------------------------------------------------------|
| id            | int      | 1                                                                          |
| nome          | string   | Guarda Chuva                                                               |
| descricao     | string   | Cor preta                                                                  |
| entregue      | boolean  | false                                                                      |
| data_cadastro | string   | 2022-01-01                                                                 |
| imagem        | string   | http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png |

**Exemplo de requisição**

```
GET /api/objetos HTTP/1.1
Host: localhost:8080
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDk1OTMsImV4cCI6MTY0MjQ1MzE5MywibmJmIjoxNjQyNDQ5NTkzLCJqdGkiOiJJelhZWHlYQ2ZkanJHV2xmIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.d7G7gx_aIrnQh1WS9T9BNiHN0ObCxmRhWnqb0tQ6w4s
Accept: */*
```

**Exemplos de respostas**

Token válido

```
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "id": 1,
    "nome": "Guarda Chuva",
    "descricao": "Cor preta",
    "entregue": false,
    "data_cadastro": "2022-01-01",
    "imagem": "http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png",
    "links": [
      {
        "type": "GET",
        "rel": "self",
        "uri": "/api/objetos/1"
      },
      {
        "type": "PUT",
        "rel": "atualizar_objeto",
        "uri": "/api/objetos/1"
      },
      {
        "type": "DELETE",
        "rel": "apagar_objeto",
        "uri": "/api/objetos/1"
      },
      {
        "type": "POST",
        "rel": "definir_imagem_objeto",
        "uri": "/api/objetos/1/imagem"
      },
      {
        "type": "PATCH",
        "rel": "definir_dono_objeto",
        "uri": "/api/objetos/1/donos"
      }
    ]
  }
]
```

Token inválido

```
HTTP/1.1 401
Content-Type: application/json

{
  "message": "Token inválido"
}
```

### Rota POST /api/objetos

**Dados da requisição**

| Campo     | Tipo   | Exemplo      |
|---------- |--------|--------------|
| nome      | string | Guarda Chuva |
| descricao | string | Cor preta    |

Regras de validação do objeto:

- `nome`: não pode ser nulo
- `nome`: não pode ser vazio
- `nome`: não pode ser menor que 3 caracteres
- `nome`: não pode ser maior que 255 caracteres
- `descricao`: não pode ser nulo
- `descricao`: não pode ser vazio
- `descricao`: não pode ser menor que 3 caracteres
- `descricao`: não pode ser maior que 255 caracteres

**Dados da resposta**

| Campo         | Tipo    | Exemplo                                                                    |
|---------------|-------- |----------------------------------------------------------------------------|
| id            | int     | 1                                                                          |
| nome          | string  | Guarda Chuva                                                               |
| descricao     | string  | Cor preta                                                                  |
| entregue      | boolean | false                                                                      |
| data_cadastro | string  | 2022-01-01                                                                 |
| imagem        | string  | http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png |

**Exemplo de requisição**

```
POST /api/objetos HTTP/1.1
Host: localhost:8080
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDk1OTMsImV4cCI6MTY0MjQ1MzE5MywibmJmIjoxNjQyNDQ5NTkzLCJqdGkiOiJJelhZWHlYQ2ZkanJHV2xmIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.d7G7gx_aIrnQh1WS9T9BNiHN0ObCxmRhWnqb0tQ6w4s
Accept: */*

{
	"nome": "Guarda Chuva",
	"descricao": "Cor preta"
}
```

**Exemplos de respostas**

Dados válidos

```
HTTP/1.1 201 OK
Content-Type: application/json

{
  "id": 1,
  "nome": "Guarda Chuva",
  "descricao": "Cor preta",
  "entregue": false,
  "data_cadastro": "2022-01-01",
  "imagem": "http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png",
  "links": [
    {
      "type": "GET",
      "rel": "self",
      "uri": "/api/objetos/1"
    },
    {
      "type": "PUT",
      "rel": "atualizar_objeto",
      "uri": "/api/objetos/1"
    },
    {
      "type": "DELETE",
      "rel": "apagar_objeto",
      "uri": "/api/objetos/1"
    },
    {
      "type": "POST",
      "rel": "definir_imagem_objeto",
      "uri": "/api/objetos/1/imagem"
    },
    {
      "type": "PATCH",
      "rel": "definir_dono_objeto",
      "uri": "/api/objetos/1/donos"
    }
  ]
}
```

Dados inválidos

```
HTTP/1.1 400
Content-Type: application/json

{
  "status": 400,
  "code": "validation_error",
  "message": "Erro de validação dos dados enviados",
  "nome": [
    "O campo nome é obrigatório."
  ]
}
```

Token inválido

```
HTTP/1.1 401
Content-Type: application/json

{
  "message": "Token inválido"
}
```

### Rota GET /api/objetos/{objetoId}

**Dados da requisição**

Não se aplica

**Dados da resposta**

| Campo         | Tipo    | Exemplo                                                                    |
|---------------|-------- |----------------------------------------------------------------------------|
| id            | int     | 1                                                                          |
| nome          | string  | Guarda Chuva                                                               |
| descricao     | string  | Cor preta                                                                  |
| entregue      | boolean | false                                                                      |
| data_cadastro | string  | 2022-01-01                                                                 |
| imagem        | string  | http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png |

**Exemplo de requisição**

```
GET /api/objetos/1 HTTP/1.1
Host: localhost:8080
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDk1OTMsImV4cCI6MTY0MjQ1MzE5MywibmJmIjoxNjQyNDQ5NTkzLCJqdGkiOiJJelhZWHlYQ2ZkanJHV2xmIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.d7G7gx_aIrnQh1WS9T9BNiHN0ObCxmRhWnqb0tQ6w4s
Accept: */*
```

**Exemplos de respostas**

Dados válidos

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "nome": "Guarda Chuva",
  "descricao": "Cor preta",
  "entregue": false,
  "data_cadastro": "2022-01-01",
  "imagem": "http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png",
  "links": [
    {
      "type": "GET",
      "rel": "self",
      "uri": "/api/objetos/1"
    },
    {
      "type": "PUT",
      "rel": "atualizar_objeto",
      "uri": "/api/objetos/1"
    },
    {
      "type": "DELETE",
      "rel": "apagar_objeto",
      "uri": "/api/objetos/1"
    },
    {
      "type": "POST",
      "rel": "definir_imagem_objeto",
      "uri": "/api/objetos/1/imagem"
    },
    {
      "type": "PATCH",
      "rel": "definir_dono_objeto",
      "uri": "/api/objetos/1/donos"
    }
  ]
}
```

Dados inválidos

```
HTTP/1.1 400
Content-Type: application/json

{
  "status": 400,
  "code": "validation_error",
  "message": "Erro de validação dos dados enviados",
  "nome": [
    "O campo nome é obrigatório."
  ]
}
```

Token inválido

```
HTTP/1.1 401
Content-Type: application/json

{
  "message": "Token inválido"
}
```

Objeto não encontrado

```
HTTP/1.1 404
Content-Type: application/json

{
  "message": "Objeto não encontrado"
}
```

### Rota PUT /api/objetos/{objetoId}

**Dados da requisição**

| Campo     | Tipo   | Exemplo      |
|---------- |--------|--------------|
| nome      | string | Guarda Chuva |
| descricao | string | Cor preta    |

Regras de validação do objeto:

- `nome`: não pode ser nulo
- `nome`: não pode ser vazio
- `nome`: não pode ser menor que 3 caracteres
- `nome`: não pode ser maior que 255 caracteres
- `descricao`: não pode ser nulo
- `descricao`: não pode ser vazio
- `descricao`: não pode ser menor que 3 caracteres
- `descricao`: não pode ser maior que 255 caracteres

**Dados da resposta**

| Campo         | Tipo    | Exemplo                                                                    |
|---------------|-------- |----------------------------------------------------------------------------|
| id            | int     | 1                                                                          |
| nome          | string  | Guarda Chuva                                                               |
| descricao     | string  | Cor preta                                                                  |
| entregue      | boolean | false                                                                      |
| data_cadastro | string  | 2022-01-01                                                                 |
| imagem        | string  | http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png |

**Exemplo de requisição**

```
PUT /api/objetos/1 HTTP/1.1
Host: localhost:8080
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDk1OTMsImV4cCI6MTY0MjQ1MzE5MywibmJmIjoxNjQyNDQ5NTkzLCJqdGkiOiJJelhZWHlYQ2ZkanJHV2xmIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.d7G7gx_aIrnQh1WS9T9BNiHN0ObCxmRhWnqb0tQ6w4s
Accept: */*

{
	"nome": "Guarda Chuva",
	"descricao": "Cor preta"
}
```

**Exemplos de respostas**

Dados válidos

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "nome": "Guarda Chuva",
  "descricao": "Cor preta",
  "entregue": false,
  "data_cadastro": "2022-01-01",
  "imagem": "http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png",
  "links": [
    {
      "type": "GET",
      "rel": "self",
      "uri": "/api/objetos/1"
    },
    {
      "type": "PUT",
      "rel": "atualizar_objeto",
      "uri": "/api/objetos/1"
    },
    {
      "type": "DELETE",
      "rel": "apagar_objeto",
      "uri": "/api/objetos/1"
    },
    {
      "type": "POST",
      "rel": "definir_imagem_objeto",
      "uri": "/api/objetos/1/imagem"
    },
    {
      "type": "PATCH",
      "rel": "definir_dono_objeto",
      "uri": "/api/objetos/1/donos"
    }
  ]
}
```

Dados inválidos

```
HTTP/1.1 400
Content-Type: application/json

{
  "status": 400,
  "code": "validation_error",
  "message": "Erro de validação dos dados enviados",
  "nome": [
    "O campo nome é obrigatório."
  ]
}
```

Token inválido

```
HTTP/1.1 401
Content-Type: application/json

{
  "message": "Token inválido"
}
```

Objeto não encontrado

```
HTTP/1.1 404
Content-Type: application/json

{
  "message": "Objeto não encontrado"
}
```

### Rota DELETE /api/objetos/{objetoId}

**Dados da requisição**

Não se aplica

**Dados da resposta**

Não se aplica

**Exemplo de requisição**

```
DELETE /api/objetos/1 HTTP/1.1
Host: localhost:8080
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDk1OTMsImV4cCI6MTY0MjQ1MzE5MywibmJmIjoxNjQyNDQ5NTkzLCJqdGkiOiJJelhZWHlYQ2ZkanJHV2xmIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.d7G7gx_aIrnQh1WS9T9BNiHN0ObCxmRhWnqb0tQ6w4s
Accept: */*
```

**Exemplos de respostas**

Dados válidos

```
HTTP/1.1 204 OK
```

Token inválido

```
HTTP/1.1 401
Content-Type: application/json

{
  "message": "Token inválido"
}
```

Objeto não encontrado

```
HTTP/1.1 404
Content-Type: application/json

{
  "message": "Objeto não encontrado"
}
```

### Rota POST /api/objetos/{objetoId}/imagem

**Dados da requisição**

| Campo         | Tipo | Exemplo |
|---------------|------|---------|
| imagem_objeto | file | -       |

Regras de validação da imagem do objeto:

- `imagem_objeto`: não pode ser nulo
- `imagem_objeto`: deve ser uma arquivo de imagem

**Dados da resposta**

| Campo    | Tipo   | Exemplo                      |
|----------|--------|------------------------------|
| mensagem | string | Imagem definida com sucesso! |

**Exemplo de requisição**

```
POST /api/objetos/1/imagem HTTP/1.1
Host: localhost:8080
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDk1OTMsImV4cCI6MTY0MjQ1MzE5MywibmJmIjoxNjQyNDQ5NTkzLCJqdGkiOiJJelhZWHlYQ2ZkanJHV2xmIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.d7G7gx_aIrnQh1WS9T9BNiHN0ObCxmRhWnqb0tQ6w4s
Accept: */*
```

**Exemplos de respostas**

Dados válidos

```
HTTP/1.1 200
Content-Type: application/json

{
  "message": "Imagem definida com sucesso!"
}
```

Dados inválidos:

```
HTTP/1.1 400
Content-Type: application/json

{
  "status": 400,
  "code": "validation_error",
  "message": "Erro de validação dos dados enviados",
  "imagem_objeto": [
    "O campo imagem objeto é obrigatório."
  ]
}
```

Token inválido

```
HTTP/1.1 401
Content-Type: application/json

{
  "message": "Token inválido"
}
```

Objeto não encontrado

```
HTTP/1.1 404
Content-Type: application/json

{
  "message": "Objeto não encontrado"
}
```

### Rota GET /api/locais/{localId}/objetos

**Dados da requisição**

Não se aplica

**Dados da resposta**

| Campo         | Tipo     | Exemplo                                                                    |
|---------------|----------|----------------------------------------------------------------------------|
| id            | int      | 1                                                                          |
| nome          | string   | Guarda Chuva                                                               |
| descricao     | string   | Cor preta                                                                  |
| data_cadastro | string   | 2022-01-01                                                                 |
| imagem        | string   | http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png |

**Exemplo de requisição**

```
GET /api/locais/1/objetos HTTP/1.1
Host: localhost:8080
Accept: */*
```

**Exemplos de respostas**

Dados válidos

```
HTTP/1.1 200
Content-Type: application/json

[
  {
    "id": 1,
    "nome": "Guarda Chuva",
    "descricao": "Cor preta",
    "data_cadastro": "2022-01-01",
    "imagem": "http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png",
  }
]
```

Local não encontrado:

```
HTTP/1.1 404
Content-Type: application/json

{
  "message": "Local não encontrado"
}
```

## Front-end

## Telas

Para esse caso de uso as tela à serem desenvolvidas são as telas de listagem de objetos e a tela com o formulário de um objeto.

### Tela de listagem de objetos

Essa tela deve conter uma tabela com o objetos do local pertencente ao usuário logado, para cada objeto deve ser exibido os botões para realizar as ações de "Editar", "Apagar", e "Informar Entrega".

![Tela de listagem dos objetos](../telas/tela-lista-de-objetos.png)

### Tela de formulário do objeto

Essa tela será utilizada tanto para cadastro quanto para edição de um objeto, ela deve conter um formulario para que se possa informar os dados do objeto a ser cadastrado ou editado.

![Tela de formulário do objeto](../telas/tela-cadastrar-objeto.png)