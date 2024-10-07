Documentação de Requisitos
Descrição do Projeto
O sistema bancário terá como objetivo principal a gestão de contas correntes e poupanças de usuários. Além das funcionalidades básicas para os usuários, o sistema contará com uma interface administrativa para gerenciar todos os aspectos do sistema, incluindo a criação, atualização e exclusão de usuários e suas respectivas contas.
Requisitos
Requisitos Funcionais
Usuário Comum (User)
Criação de Conta (Create Account): O usuário poderá criar contas correntes ou poupanças, fornecendo os dados pessoais solicitados.
Visualização de Contas (View Accounts): O usuário poderá visualizar o saldo e histórico de transações de suas contas.
Exclusão de Conta (Delete Account): O usuário poderá solicitar a exclusão de uma conta, desde que não haja pendências financeiras.
Administrador (Admin)
Gerenciamento de Usuários (Manage Users): O administrador poderá:
Criar novos usuários.
Editar informações de usuários existentes (nome, e-mail, etc.).
Excluir usuários.
Gerenciamento de Contas (Manage Accounts): O administrador poderá:
Visualizar todas as contas do sistema.
Criar contas para usuários.
Editar informações de contas (tipo, saldo, etc.).
Excluir contas.
Relatórios (Reports): O administrador poderá gerar relatórios sobre as atividades do sistema, como número de contas, valor total em depósitos, etc.
Requisitos Não Funcionais
Segurança (Security): O sistema deverá implementar medidas de segurança robustas, como criptografia e controle de acesso.
Desempenho (Performance): O sistema deverá responder de maneira eficiente às solicitações dos usuários, especialmente em transações financeiras.
Disponibilidade (Availability): O sistema deverá ser altamente disponível, com tempo de inatividade mínimo.
Usabilidade (Usability): A interface deverá ser intuitiva, fácil de usar tanto para o usuário comum quanto para o administrador.
Escalabilidade (Scalability): O sistema deverá ser capaz de lidar com o aumento no número de usuários e transações.

Diagrama UML
User
Atributos: name, email, listOfAccounts
Métodos: createAccount(), viewAccounts(), deleteAccount()
Admin
Herdado de: User
Atributos/Métodos: permissions (CRUD users and accounts), generateReports()
Account (Interface)
Métodos: withdraw(), deposit(), transfer()
CheckingAccount (Conta Corrente)
Implementa: Account
Atributos: withdrawalLimit, maintenanceFee
SavingsAccount (Conta Poupança)
Implementa: Account
Atributos: interestRate
Transaction
Atributos: date, value, type (withdrawal, deposit, transfer), originAccount, destinationAccount
Associações e Heranças:
User tem muitos Account.
Admin é uma herança de User.
CheckingAccount e SavingsAccount implementam Account.
Transaction está associada às contas (origin e destination).


Arquitetura do Sistema
Camadas do Sistema
Front-end (View):
Linguagens: HTML, CSS, JavaScript.
Biblioteca de Estilo: Bootstrap.
Responsabilidade: Interface com o usuário, exibindo as informações enviadas pelo back-end e capturando as interações do usuário.
Integração: A interface se comunica com o back-end por meio de requisições HTTP, utilizando AJAX para interações dinâmicas.
Back-end (Controller e Model):
Framework: Spring Boot.
Linguagem: Java.
Padrão: MVC.
Responsabilidade: Manipulação de regras de negócio e controle de fluxo de dados. Processamento de requisições de clientes (usuários comuns e administradores), incluindo operações de CRUD e transações bancárias.
Segurança: Implementação de autenticação e autorização para controlar o acesso às funcionalidades (usuário comum vs. administrador).
Integração com Banco de Dados: Persistência de dados com MongoDB.
Controle de Versionamento: Git.
Banco de Dados (Model):
Banco de Dados: MongoDB (NoSQL).
Estrutura de Dados:
Coleções: Usuários, Contas (Corrente e Poupança), Transações.
Índices: Definidos para otimizar a busca de usuários, contas e histórico de transações.
Modelo de Dados: Cada usuário poderá ter uma ou mais contas (corrente ou poupança). O administrador poderá manipular os dados de todos os usuários e contas.
Fluxo de Dados
Criação de Conta (Usuário Comum):
O usuário faz uma solicitação para criar uma conta (corrente ou poupança) via interface.
O back-end processa a solicitação, cria a conta e armazena os dados no MongoDB.
O front-end exibe a confirmação da criação da conta.
Autenticação e Acesso (Admin e Usuário):
Ao realizar login, o sistema valida as credenciais e verifica o nível de permissão (usuário ou admin).
O admin terá acesso a funcionalidades adicionais, como gerenciamento de usuários e contas.
Transações Bancárias (Usuário Comum):
O usuário pode realizar operações como depósitos, saques ou transferências.
Cada operação cria uma transação registrada no banco de dados, com referência ao saldo atual e às contas envolvidas.
CRUD para Usuários e Contas (Admin):
O administrador poderá criar, editar ou excluir usuários e contas. Todas as operações são registradas no sistema, e o banco de dados é atualizado em tempo real.
Detalhamento dos Módulos Back-End
Módulo de Autenticação:
Implementação de autenticação usando JWT (JSON Web Tokens) para manter sessões seguras.
Controle de acesso a rotas específicas, conforme as permissões de usuário.
Módulo de Transações:
Gerenciamento de todas as operações financeiras, incluindo depósitos, saques e transferências.
Verificação de saldo disponível, limites de saque e validação de transações.
Registro de transações no banco de dados, para histórico.
Módulo de Contas:
CRUD de contas correntes e poupanças, permitindo ao usuário comum criar e gerenciar suas próprias contas, e ao administrador manipular todas as contas do sistema.
Módulo de Relatórios (Admin):
Geração de relatórios detalhados sobre o número de usuários, valor total em depósitos e outras estatísticas de uso do sistema.

Segurança
Autenticação e Autorização:
A autenticação será realizada com JWT para garantir segurança nas sessões de usuários.
O administrador terá permissões adicionais para manipular os dados de todos os usuários e contas.
Proteção de Dados:
Criptografia será aplicada aos dados sensíveis (ex.: senhas).
Logs serão gerados para auditoria e troubleshooting.

Escalabilidade
Estratégias de Escalabilidade:
Balanceamento de Carga: Utilizar uma infraestrutura escalável, caso o sistema precise suportar um grande número de usuários simultâneos.
Replicação de Dados: MongoDB permite a replicação para aumentar a disponibilidade e distribuição de dados.

Manutenção e Padrões
Controle de Versionamento:
O versionamento do código será gerido pelo Git, com branches para desenvolvimento, testes e produção.
Docker:
Docker será usado para criar ambientes de desenvolvimento e testes consistentes, garantindo que o sistema funcione da mesma forma em todas as máquinas.
Padrões de Projeto:
MVC para a separação de responsabilidades.
REST para a comunicação entre front-end e back-end.
Gerenciamento de Dependências:
Utilização do Maven para gerenciar bibliotecas e dependências externas.

Documentação da API (Swagger/OpenAPI)
1. Descrição Geral
A API do sistema bancário segue os princípios REST, expondo endpoints para o gerenciamento de contas e transações, além de funcionalidades administrativas. A documentação da API é gerada automaticamente utilizando Swagger e está disponível diretamente via uma interface gráfica, acessível através do endpoint /swagger-ui.html.

2. Endpoints
2.1. Usuários
POST /users
Cria um novo usuário no sistema.
Corpo da Requisição (JSON):
json
Copy code
{
  "name": "John Doe",
  "email": "johndoe@example.com",
  "password": "password123"
}
Resposta:
201 Created: O usuário foi criado com sucesso.
400 Bad Request: Se os dados fornecidos forem inválidos.
GET /users/{id}
Retorna os dados de um usuário específico com base no ID.
Resposta:
200 OK: Dados do usuário.
404 Not Found: Se o usuário não for encontrado.
DELETE /users/{id}
Remove um usuário específico com base no ID.
Resposta:
200 OK: O usuário foi removido com sucesso.
404 Not Found: Se o usuário não for encontrado.
2.2. Contas
POST /accounts
Cria uma nova conta corrente ou poupança para um usuário.
Corpo da Requisição (JSON):
json
Copy code
{
  "userId": "12345",
  "type": "checking", // ou "savings"
  "initialDeposit": 500.00
}
Resposta:
201 Created: A conta foi criada com sucesso.
400 Bad Request: Se os dados fornecidos forem inválidos.
GET /accounts/{id}
Retorna os dados de uma conta específica.
Resposta:
200 OK: Dados da conta.
404 Not Found: Se a conta não for encontrada.
2.3. Transações
POST /transactions
Cria uma nova transação (depósito, saque ou transferência).
Corpo da Requisição (JSON):
json
Copy code
{
  "accountId": "67890",
  "type": "deposit", // ou "withdraw" ou "transfer"
  "amount": 100.00,
  "targetAccountId": "12345" // Apenas para transferências
}
Resposta:
201 Created: A transação foi realizada com sucesso.
400 Bad Request: Se houver um erro, como saldo insuficiente.
GET /transactions/{id}
Retorna os dados de uma transação específica.
Resposta:
200 OK: Dados da transação.
404 Not Found: Se a transação não for encontrada.

3. Estrutura de Dados
Usuário:
json
Copy code
{
  "id": "string",
  "name": "string",
  "email": "string",
  "password": "string"
}


Conta:
json
Copy code
{
  "id": "string",
  "userId": "string",
  "type": "string", // "checking" ou "savings"
  "balance": "number"
}


Transação:
json
Copy code
{
  "id": "string",
  "accountId": "string",
  "type": "string", // "deposit", "withdraw", "transfer"
  "amount": "number",
  "date": "string",
  "targetAccountId": "string" // Apenas para transferências
}



4. Exemplos de Requisições
4.1. Exemplo de Requisição para Criar Usuário (POST /users)
Requisição:
http
Copy code
POST /users
Content-Type: application/json


{
  "name": "Jane Doe",
  "email": "janedoe@example.com",
  "password": "securepassword"
}

Resposta:
http
Copy code
HTTP/1.1 201 Created
Location: /users/12345

4.2. Exemplo de Requisição para Listar Contas (GET /accounts)
Requisição:
http
Copy code
GET /accounts/12345

Resposta:
http
Copy code
HTTP/1.1 200 OK
Content-Type: application/json


{
  "id": "12345",
  "userId": "67890",
  "type": "checking",
  "balance": 1000.00
}


5. Implementação do Swagger no Spring Boot
Para habilitar o Swagger no Spring Boot, você pode adicionar as dependências necessárias no pom.xml e configurar o Swagger na classe principal do projeto:
Dependências Maven:
xml
Copy code
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-boot-starter</artifactId>
    <version>3.0.0</version>
</dependency>

Configuração:
java
Copy code
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

Após isso, a documentação interativa da API estará disponível no endereço /swagger-ui.html.

6. Formato de Dados e Padrões de Respostas
As trocas de dados entre o front-end e o back-end serão feitas utilizando o formato JSON, tanto nas requisições quanto nas respostas. A API seguirá os códigos de status HTTP padrão para indicar o sucesso ou falha das operações (ex.: 200 OK, 201 Created, 400 Bad Request, 404 Not Found).



5. Plano de Testes
Inclui os testes que serão feitos para garantir que o sistema funciona conforme o esperado. No início, podem ser testes manuais (testando funcionalidades principais), mas ao longo do tempo podem ser automatizados.
Seções principais:
Casos de Teste: Por exemplo, “Adicionar nova conta corrente” com os passos e o resultado esperado.
Testes de Integração: Como o sistema deve se comportar ao integrar com o MongoDB ou Docker.
Testes de Performance: Se necessário, como o sistema se comporta em termos de tempo de resposta.
Organização do Projeto
Para organizar o projeto dentro do Spring Boot, incluindo o front-end, MongoDB e Docker, aqui está um esquema inicial de pastas e arquivos:
Estrutura de Pastas do Projeto

src/
|-- main/
|   |-- java/
|       |-- com/
|           |-- seu_projeto/
|               |-- controller/
|                   |-- UsuarioController.java
|                   |-- ContaController.java
|                   |-- AdminController.java
|               |-- model/
|                   |-- Usuario.java
|                   |-- Conta.java
|                   |-- ContaCorrente.java
|                   |-- ContaPoupanca.java
|                   |-- Transacao.java
|               |-- repository/
|                   |-- UsuarioRepository.java
|                   |-- ContaRepository.java
|                   |-- TransacaoRepository.java
|               |-- service/
|                   |-- UsuarioService.java
|                   |-- ContaService.java
|                   |-- TransacaoService.java
|               |-- config/
|                   |-- SwaggerConfig.java
|                   |-- SecurityConfig.java
|-- resources/
|   |-- static/
|   |   |-- css/
|   |   |-- js/
|   |-- templates/
|       |-- home.html
|       |-- admin_dashboard.html
|       |-- user_dashboard.html
|-- test/
|   |-- java/
|       |-- com/
|           |-- seu_projeto/
|               |-- service/
|                   |-- UsuarioServiceTest.java
|                   |-- ContaServiceTest.java
|                   |-- TransacaoServiceTest.java
|-- Dockerfile
|-- docker-compose.yml



Documentação Essencial a Criar:
README.md: Resumo inicial do projeto, como instalar, como rodar, e breve explicação sobre suas funcionalidades.
docs/:
requisitos.md: Requisitos do sistema (funcionais e não funcionais).
uml_diagramas/: Diagramas UML (classes, componentes).
api_documentacao.md: Descrição das rotas e exemplos de APIs.
arquitetura.md: Explicação da arquitetura, componentes e interações.
plano_de_testes.md: Plano de testes com casos de teste descritos.


