
1. Endpoint RESTful

O endpoint criado segue o padrão RESTful e tem a função de retornar todos os eventos registrados no sistema.

Rota:
`GET /eventos`

Esse recurso é protegido por um middleware de autenticação, que exige que o cliente envie um token JWT válido no cabeçalho da requisição.

Exemplo de requisição:

```
GET /eventos
Authorization: Bearer <token_jwt>
```

Exemplo de resposta:

```json
{
  "data": [
    { "id": "1", "name": "Meetup NodeJS", "date": "2025-11-10" },
    { "id": "2", "name": "Workshop GraphQL", "date": "2025-12-02" },
    { "id": "3", "name": "Hackathon API Navigator", "date": "2026-01-15" }
  ],
  "user": { "id": 1, "name": "Usuário Autenticado" }
}
```

---

2. Consulta GraphQL

O endpoint GraphQL foi definido em:
`/graphql`

A consulta abaixo busca apenas o nome e a data de um evento específico:

```graphql
query {
  evento(id: "2") {
    name
    date
  }
}
```

Resposta esperada:

```json
{
  "data": {
    "evento": {
      "name": "Workshop GraphQL",
      "date": "2025-12-02"
    }
  }
}


Por que o GraphQL é mais eficiente?

Em uma API REST, todos os campos de todos os eventos são retornados, mesmo que o cliente precise de poucas informações.
Já o GraphQL permite consultar somente os dados necessários, reduzindo o volume de tráfego e o processamento no servidor.
 Dessa forma, o GraphQL torna as requisições mais ágeis, otimizadas e personalizadas para cada necessidade.


3. Autenticação e Segurança com JWT

O JWT (JSON Web Token) é utilizado para controlar o acesso aos recursos da API e garantir a segurança das operações.

Fluxo de autenticação:

1. O usuário realiza o login pelo endpoint:
   `POST /login`
2. O servidor cria um token JWT contendo informações básicas do usuário, como:
   `{ "userId": 1, "username": "teste_user" }`
3. Esse token é assinado com uma chave secreta e enviado de volta ao cliente.
4. Nas requisições seguintes, o cliente envia o token no cabeçalho:
   `Authorization: Bearer <token>`
5. O middleware do servidor valida o token antes de liberar o acesso a rotas protegidas, como `/eventos`.

Esse processo assegura que somente usuários autenticados possam acessar informações restritas, reproduzindo o comportamento de sistemas de autenticação reais.

4. Reflexão sobre Cooperação

Em integrações que envolvem autenticação, como OAuth e JWT, a colaboração entre as equipes de front-end e back-end é fundamental.

* O trabalho conjunto garante que todos compreendam como o token é criado, validado e transmitido, evitando erros de autenticação.
 A comunicação clara e assertiva é essencial para definir padrões de segurança, como o tempo de expiração e o formato dos tokens.
 A cooperação técnica reduz falhas, evita retrabalhos e promove uma integração mais estável e segura entre os serviços.

Em síntese: trabalhar de forma colaborativa fortalece a segurança, melhora a integração e eleva a qualidade do produto final.


Conclusão

O projeto API Navigator exemplifica como combinar RESTful, GraphQL e JWT para criar uma API **moderna, eficiente e segura.
Além da parte técnica, o projeto reforça a importância da colaboração entre equipes no desenvolvimento, garantindo **entregas consistentes, seguras e de alta qualidade.

Deseja que eu **formate esse texto como um relatório pronto para entrega (em PDF ou DOCX)**? Posso deixá-lo com capa, seções e layout de caderno.
