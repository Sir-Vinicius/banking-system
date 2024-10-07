## Documentação da API (Swagger/OpenAPI)

Nesta seção, você encontrará a documentação detalhada da API do sistema bancário, que segue os princípios REST. A API fornece endpoints para o gerenciamento de contas e transações, além de funcionalidades administrativas. A documentação é gerada automaticamente utilizando Swagger, permitindo que você acesse uma interface gráfica por meio do endpoint `/swagger-ui.html`. 

## Links para a documentação

- [README](../README.md)
- [Requisitos do Sistema](docs/requisitos.md)
- [Diagramas UML](docs/uml.md)
- [Documentação da API](docs/api_documentacao.md)
- [Arquitetura do Sistema](docs/arquitetura.md)
- [Plano de Testes](docs/plano_de_testes.md)

### 1. Descrição Geral
A API do sistema bancário segue os princípios REST, expondo endpoints para o gerenciamento de contas e transações, além de funcionalidades administrativas. A documentação da API é gerada automaticamente utilizando Swagger e está disponível diretamente via uma interface gráfica, acessível através do endpoint `/swagger-ui.html`.

### 2. Endpoints

#### 2.1. Usuários
- **POST /users**
  - Cria um novo usuário no sistema.
  - **Corpo da Requisição (JSON)**:
    ```json
    {
      "name": "John Doe",
      "email": "johndoe@example.com",
      "password": "password123"
    }
    ```
  - **Resposta**:
    - `201 Created`: O usuário foi criado com sucesso.
    - `400 Bad Request`: Se os dados fornecidos forem inválidos.

- **GET /users/{id}**
  - Retorna os dados de um usuário específico com base no ID.
  - **Resposta**:
    - `200 OK`: Dados do usuário.
    - `404 Not Found`: Se o usuário não for encontrado.

- **DELETE /users/{id}**
  - Remove um usuário específico com base no ID.
  - **Resposta**:
    - `200 OK`: O usuário foi removido com sucesso.
    - `404 Not Found`: Se o usuário não for encontrado.

#### 2.2. Contas
- **POST /accounts**
  - Cria uma nova conta corrente ou poupança para um usuário.
  - **Corpo da Requisição (JSON)**:
    ```json
    {
      "userId": "12345",
      "type": "checking", // ou "savings"
      "initialDeposit": 500.00
    }
    ```
  - **Resposta**:
    - `201 Created`: A conta foi criada com sucesso.
    - `400 Bad Request`: Se os dados fornecidos forem inválidos.

- **GET /accounts/{id}**
  - Retorna os dados de uma conta específica.
  - **Resposta**:
    - `200 OK`: Dados da conta.
    - `404 Not Found`: Se a conta não for encontrada.

#### 2.3. Transações
- **POST /transactions**
  - Cria uma nova transação (depósito, saque ou transferência).
  - **Corpo da Requisição (JSON)**:
    ```json
    {
      "accountId": "67890",
      "type": "deposit", // ou "withdraw" ou "transfer"
      "amount": 100.00,
      "targetAccountId": "12345" // Apenas para transferências
    }
    ```
  - **Resposta**:
    - `201 Created`: A transação foi realizada com sucesso.
    - `400 Bad Request`: Se houver um erro, como saldo insuficiente.

- **GET /transactions/{id}**
  - Retorna os dados de uma transação específica.
  - **Resposta**:
    - `200 OK`: Dados da transação.
    - `404 Not Found`: Se a transação não for encontrada.

### 3. Estrutura de Dados
**Usuário:**
```json
{
  "id": "string",
  "name": "string",
  "email": "string",
  "password": "string"
}
```

**Conta:**
```json
{
  "id": "string",
  "userId": "string",
  "type": "string", // "checking" ou "savings"
  "balance": "number"
}
```

**Transação:**
```json
{
  "id": "string",
  "accountId": "string",
  "type": "string", // "deposit", "withdraw", "transfer"
  "amount": "number",
  "date": "string",
  "targetAccountId": "string" // Apenas para transferências
}
```


### 4. Exemplos de Requisições
#### 4.1. Exemplo de Requisição para Criar Usuário (POST /users)
Requisição:
```http
POST /users
Content-Type: application/json


{
  "name": "Jane Doe",
  "email": "janedoe@example.com",
  "password": "securepassword"
}
```
Resposta:
```http
HTTP/1.1 201 Created
Location: /users/12345
```
#### 4.2. Exemplo de Requisição para Listar Contas (GET /accounts)
Requisição:
```http
GET /accounts/12345
```
Resposta:
```http
HTTP/1.1 200 OK
Content-Type: application/json


{
  "id": "12345",
  "userId": "67890",
  "type": "checking",
  "balance": 1000.00
}
```

### 5. Implementação do Swagger no Spring Boot
Para habilitar o Swagger no Spring Boot, você pode adicionar as dependências necessárias no pom.xml e configurar o Swagger na classe principal do projeto:
**Dependências Maven:**
```xml
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-boot-starter</artifactId>
    <version>3.0.0</version>
</dependency>
```
**Configuração:**
```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import springfox.documentation.builders.PathSelectors;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.Docket;

@Configuration
public class SwaggerConfig {


    @Bean
    public Docket api() {
        return new Docket(DocumentationType.SWAGGER_2)
                .select()
                .apis(RequestHandlerSelectors.any())
                .paths(PathSelectors.any())
                .build();
    }
}
```
Após isso, a documentação interativa da API estará disponível no endereço /swagger-ui.html.

### 6. Formato de Dados e Padrões de Respostas
As trocas de dados entre o front-end e o back-end serão feitas utilizando o formato JSON, tanto nas requisições quanto nas respostas. A API seguirá os códigos de status HTTP padrão para indicar o sucesso ou falha das operações (ex.: 200 OK, 201 Created, 400 Bad Request, 404 Not Found).
