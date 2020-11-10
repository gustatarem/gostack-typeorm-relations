
<img alt="GoStack" src="https://storage.googleapis.com/golden-wind/bootcamp-gostack/header-desafios-new.png" />

<h3 align="center">
  Desafio 09: Relacionamentos com banco de dados no Node.js
</h3>

## :rocket: Sobre o desafio

Essa é uma aplicação que permite a criação de clientes, produtos e pedidos, onde o cliente pode gerar novos pedidos de compra de certos produtos, como um pequeno e-commerce.

## :motorway: Rotas da aplicação

- **`POST /customers`**: A rota recebe `name` e `email` dentro do corpo da requisição, sendo o `name` o nome do cliente a ser cadastrado. Ao cadastrar um novo cliente, ele é armazenado dentro do seu banco de dados e retorna-se o cliente criado. Ao cadastrar no banco de dados, a tabela `customers` possuirá os campos `name`, `email`, `created_at`, `updated_at`.

- **`POST /products`**: Essa rota recebe `name`, `price` e `quantity` dentro do corpo da requisição, sendo o `name` o nome do produto a ser cadastrado, `price` o valor unitário e `quantity` a quantidade existente em estoque do produto. Com esses dados é criado no banco de dados um novo produto com os seguintes campos: `name`, `price`, `quantity`, `created_at`, `updated_at`.

- **`POST /orders/`**: Essa rota você recebe no corpo da requisição o `customer_id` e um array de products, contendo o `id` e a `quantity` que você deseja adicionar a um novo pedido. Aqui é cadastrado na tabela `order` um novo pedido, que estará relacionado ao `customer_id` informado, `created_at` e `updated_at` . Já na tabela `orders_products`, você deve armazenar o `product_id`, `order_id`, `price` e `quantity`, `created_at` e `updated_at`.

**Exemplo de envio de requisição**:

```json
{
  "customer_id": "e26f0f2a-3ac5-4c21-bd22-671119adf4e9",
  "products": [
    {
      "id": "ce0516f3-63ae-4048-9a8a-8b6662281efe",
      "quantity": 5
    },
    {
      "id": "82612f2b-3f31-40c6-803d-c2a95ef35e7c",
      "quantity": 7
    }
  ]
}
```

**Exemplo de retorno**:

```json
{
  "id": "5cbc4aa2-b3dc-43f9-b121-44c1e416fa92",
  "created_at": "2020-05-11T07:09:48.767Z",
  "updated_at": "2020-05-11T07:09:48.767Z",
  "customer": {
    "id": "e26f0f2a-3ac5-4c21-bd22-671119adf4e9",
    "name": "Rocketseat",
    "email": "oi@rocketseat.com.br",
    "created_at": "2020-05-11T06:20:28.729Z",
    "updated_at": "2020-05-11T06:20:28.729Z"
  },
  "order_products": [
    {
      "product_id": "ce0516f3-63ae-4048-9a8a-8b6662281efe",
      "price": "1400.00",
      "quantity": 5,
      "order_id": "5cbc4aa2-b3dc-43f9-b121-44c1e416fa92",
      "id": "265b6cbd-3ab9-421c-b358-c2e2b5b3b542",
      "created_at": "2020-05-11T07:09:48.767Z",
      "updated_at": "2020-05-11T07:09:48.767Z"
    },
    {
      "product_id": "82612f2b-3f31-40c6-803d-c2a95ef35e7c",
      "price": "500.00",
      "quantity": 7,
      "order_id": "5cbc4aa2-b3dc-43f9-b121-44c1e416fa92",
      "id": "ae37bcd6-7be7-47b9-b277-afee35aab4e4",
      "created_at": "2020-05-11T07:09:48.767Z",
      "updated_at": "2020-05-11T07:09:48.767Z"
    }
  ]
}
```

- **`GET /orders/:id`**: Essa rota retorna as informações de um pedido específico, com todas as informações que podem ser recuperadas através dos relacionamentos entre a tabela `orders`, `customers` e `orders_products`.

## :computer: Instruções de instalação e teste

Clone o repositório usando o `git` ou faça o download no formato zip. 
Antes de tudo, certifique-se de que você tem um gerenciador de pacotes (como o yarn), o `Node.js` e o Docker (com a imagem PostgreSQL) instalados em sua máquina.

Com o Docker rodando, entre no seu gerenciador de banco de dados de preferência e crie 2 databases:

- **`gostack_desafio09`**
- **`gostack_desafio09_tests`**

Após baixar o projeto, abra uma aba do terminal e execute os seguintes comandos:

```Bash
# ../pasta-de-destino
$ cd gostack-typeorm-relations
# ../pasta-de-destino/gostack-typeorm-relations
$ yarn
```

Para rodar as migrations e criar as tabelas no banco de dados:

```Bash
# ../pasta-de-destino/gostack-typeorm-relations
$ yarn typeorm migration:run
```

Para iniciar a aplicação na porta 3333:

```Bash
# ../pasta-de-destino/gostack-typeorm-relations
$ yarn dev:server
```

Para rodar os testes da aplicação (utilizando a database gostack_desafio06_tests criada anteriormente):

```Bash
# ../pasta-de-destino/gostack-typeorm-relations
$ yarn test
```
