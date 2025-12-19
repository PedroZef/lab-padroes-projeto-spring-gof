# Explorando Padrões de Projetos na Prática com Java

Repositório com as implementações dos padrões de projeto explorados no Lab "Explorando Padrões de Projetos na Prática com Java". Especificamente, este projeto explorou alguns padrões usando o Spring Framework, são eles:

- Singleton
- Strategy/Repository
- Facade

## API Endpoints

Esta aplicação fornece uma API REST para gerenciar Clientes.

### Clientes

A API de Clientes (`/clientes`) permite realizar um CRUD completo de clientes. A integração com a API [ViaCEP](https://viacep.com.br/) é feita de forma transparente ao criar ou atualizar um cliente.

#### `GET /clientes`

Retorna uma lista de todos os clientes cadastrados.

#### `GET /clientes/{id}`

Retorna os detalhes de um cliente específico com base no seu `id`.

#### `POST /clientes`

Cria um novo cliente. O corpo da requisição deve conter os dados do cliente, incluindo seu endereço com o CEP.

**Exemplo de corpo de requisição:**

```json
{
    "nome": "Fulano de Tal",
    "endereco": {
        "cep": "01001-000"
    }
}
```

**Comportamento da Integração (Facade):**

- Ao receber a requisição, o sistema verifica se o `Endereco` para o CEP fornecido já existe no banco de dados local.
- Se o `Endereco` não existir, o sistema consulta a API do ViaCEP para obter os dados completos do endereço.
- O `Endereco` retornado pelo ViaCEP é salvo no banco de dados local.
- O novo `Cliente` é salvo com a referência ao `Endereco` (seja o que já existia ou o que foi recém-criado).

#### `PUT /clientes/{id}`

Atualiza os dados de um cliente existente. O comportamento da integração com o ViaCEP é o mesmo do endpoint `POST`.

#### `DELETE /clientes/{id}`

Exclui um cliente do banco de dados com base no seu `id`.

## Como Executar o Projeto

Para executar este projeto localmente, siga os passos abaixo:

1. **Clone o repositório:**

    ```bash
    git clone [https://github.com/digitalinnovationone/lab-padroes-projeto-spring-gof.git] e cd lab-padroes-projeto-spring-gof

    ```

2. **Execute a aplicação:**

    Utilize o Maven Wrapper para iniciar a aplicação Spring Boot.

    ```bash
    .\mvnw.cmd spring-boot:run
    ```

    A API estará disponível em `http://localhost:8080`.

    Com o Swagger-ui em `http://localhost:8080/swagger-ui/index.html`.

## Como Contribuir

Ajustes e melhorias são sempre bem-vindos! Se você tem alguma sugestão para aprimorar este projeto, sinta-se à vontade para seguir estes passos:

1. Faça um **Fork** do projeto.
2. Crie uma nova **Branch** (`git checkout -b feature/sua-feature`).
3. Faça **Commit** de suas alterações (`git commit -m 'Adiciona sua feature'`).
4. Faça **Push** para a Branch (`git push origin feature/sua-feature`).
5. Abra um **Pull Request**.
