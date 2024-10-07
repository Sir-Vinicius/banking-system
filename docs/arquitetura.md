## Arquitetura do Sistema

Esta seção descreve a arquitetura do sistema bancário, incluindo as camadas do sistema, fluxo de dados, módulos de back-end e estratégias de segurança e escalabilidade. O objetivo é proporcionar uma visão clara da estrutura e funcionamento do sistema.

## Links para a documentação

- [README](../README.md)
- [Requisitos do Sistema](docs/requisitos.md)
- [Diagramas UML](docs/uml.md)
- [Documentação da API](docs/api_documentacao.md)
- [Arquitetura do Sistema](docs/arquitetura.md)
- [Plano de Testes](docs/plano_de_testes.md)

### Camadas do Sistema

#### Front-end (View)
- **Linguagens**: HTML, CSS, JavaScript.
- **Biblioteca de Estilo**: Bootstrap.
- **Responsabilidade**: Interface com o usuário, exibindo as informações enviadas pelo back-end e capturando as interações do usuário.
- **Integração**: A interface se comunica com o back-end por meio de requisições HTTP, utilizando AJAX para interações dinâmicas.

#### Back-end (Controller e Model)
- **Framework**: Spring Boot.
- **Linguagem**: Java.
- **Padrão**: MVC.
- **Responsabilidade**: Manipulação de regras de negócio e controle de fluxo de dados. Processamento de requisições de clientes (usuários comuns e administradores), incluindo operações de CRUD e transações bancárias.
- **Segurança**: Implementação de autenticação e autorização para controlar o acesso às funcionalidades (usuário comum vs. administrador).
- **Integração com Banco de Dados**: Persistência de dados com MongoDB.
- **Controle de Versionamento**: Git.

#### Banco de Dados (Model)
- **Banco de Dados**: MongoDB (NoSQL).
- **Estrutura de Dados**:
  - **Coleções**: Usuários, Contas (Corrente e Poupança), Transações.
  - **Índices**: Definidos para otimizar a busca de usuários, contas e histórico de transações.
  - **Modelo de Dados**: Cada usuário poderá ter uma ou mais contas (corrente ou poupança). O administrador poderá manipular os dados de todos os usuários e contas.

### Fluxo de Dados
- **Criação de Conta (Usuário Comum)**:
  1. O usuário faz uma solicitação para criar uma conta (corrente ou poupança) via interface.
  2. O back-end processa a solicitação, cria a conta e armazena os dados no MongoDB.
  3. O front-end exibe a confirmação da criação da conta.

- **Autenticação e Acesso (Admin e Usuário)**:
  1. Ao realizar login, o sistema valida as credenciais e verifica o nível de permissão (usuário ou admin).
  2. O admin terá acesso a funcionalidades adicionais, como gerenciamento de usuários e contas.

- **Transações Bancárias (Usuário Comum)**:
  1. O usuário pode realizar operações como depósitos, saques ou transferências.
  2. Cada operação cria uma transação registrada no banco de dados, com referência ao saldo atual e às contas envolvidas.

- **CRUD para Usuários e Contas (Admin)**:
  1. O administrador poderá criar, editar ou excluir usuários e contas. Todas as operações são registradas no sistema, e o banco de dados é atualizado em tempo real.

### Detalhamento dos Módulos Back-End

#### Módulo de Autenticação
- Implementação de autenticação usando JWT (JSON Web Tokens) para manter sessões seguras.
- Controle de acesso a rotas específicas, conforme as permissões de usuário.

#### Módulo de Transações
- Gerenciamento de todas as operações financeiras, incluindo depósitos, saques e transferências.
- Verificação de saldo disponível, limites de saque e validação de transações.
- Registro de transações no banco de dados, para histórico.

#### Módulo de Contas
- CRUD de contas correntes e poupanças, permitindo ao usuário comum criar e gerenciar suas próprias contas, e ao administrador manipular todas as contas do sistema.

#### Módulo de Relatórios (Admin)
- Geração de relatórios detalhados sobre o número de usuários, valor total em depósitos e outras estatísticas de uso do sistema.

## Segurança

### Autenticação e Autorização
- A autenticação será realizada com JWT para garantir segurança nas sessões de usuários.
- O administrador terá permissões adicionais para manipular os dados de todos os usuários e contas.

### Proteção de Dados
- Criptografia será aplicada aos dados sensíveis (ex.: senhas).
- Logs serão gerados para auditoria e troubleshooting.

## Escalabilidade

### Estratégias de Escalabilidade
- **Balanceamento de Carga**: Utilizar uma infraestrutura escalável, caso o sistema precise suportar um grande número de usuários simultâneos.
- **Replicação de Dados**: MongoDB permite a replicação para aumentar a disponibilidade e distribuição de dados.

## Manutenção e Padrões

### Controle de Versionamento
- O versionamento do código será gerido pelo Git, com branches para desenvolvimento, testes e produção.

### Docker
- Docker será usado para criar ambientes de desenvolvimento e testes consistentes, garantindo que o sistema funcione da mesma forma em todas as máquinas.

### Padrões de Projeto
- MVC para a separação de responsabilidades.
- REST para a comunicação entre front-end e back-end.

### Gerenciamento de Dependências
- Utilização do Maven para gerenciar bibliotecas e dependências externas.

## Organização do Projeto

Para organizar o projeto dentro do Spring Boot, incluindo o front-end, MongoDB e Docker, aqui está um esquema inicial de pastas e arquivos:

### Estrutura de Pastas do Projeto
```scss
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
```

## Documentação Essencial a Criar

- **README.md**: Resumo inicial do projeto, como instalar, como rodar, e breve explicação sobre suas funcionalidades.
- **docs/**:
  - **requisitos.md**: Requisitos do sistema (funcionais e não funcionais).
  - **uml_diagramas/**: Diagramas UML (classes, componentes).
  - **api_documentacao.md**: Descrição das rotas e exemplos de APIs.
  - **arquitetura.md**: Explicação da arquitetura, componentes e interações.
  - **plano_de_testes.md**: Plano de testes com casos de teste descritos.
