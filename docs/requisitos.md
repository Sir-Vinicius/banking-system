## Requisitos do Sistema

Nesta seção, descrevemos os requisitos funcionais e não funcionais do sistema.

## Links para a documentação

- [README](../README.md)
- [Requisitos do Sistema](docs/requisitos.md)
- [Diagramas UML](docs/uml.md)
- [Documentação da API](docs/api_documentacao.md)
- [Arquitetura do Sistema](docs/arquitetura.md)
- [Plano de Testes](docs/plano_de_testes.md)

### Requisitos Funcionais

#### Usuário Comum (User)
- **Criação de Conta (Create Account)**: O usuário poderá criar contas correntes ou poupanças, fornecendo os dados pessoais solicitados.
- **Visualização de Contas (View Accounts)**: O usuário poderá visualizar o saldo e histórico de transações de suas contas.
- **Exclusão de Conta (Delete Account)**: O usuário poderá solicitar a exclusão de uma conta, desde que não haja pendências financeiras.

#### Administrador (Admin)
- **Gerenciamento de Usuários (Manage Users)**: O administrador poderá:
  - Criar novos usuários.
  - Editar informações de usuários existentes (nome, e-mail, etc.).
  - Excluir usuários.
- **Gerenciamento de Contas (Manage Accounts)**: O administrador poderá:
  - Visualizar todas as contas do sistema.
  - Criar contas para usuários.
  - Editar informações de contas (tipo, saldo, etc.).
  - Excluir contas.
- **Relatórios (Reports)**: O administrador poderá gerar relatórios sobre as atividades do sistema, como número de contas, valor total em depósitos, etc.

### Requisitos Não Funcionais
- **Segurança (Security)**: O sistema deverá implementar medidas de segurança robustas, como criptografia e controle de acesso.
- **Desempenho (Performance)**: O sistema deverá responder de maneira eficiente às solicitações dos usuários, especialmente em transações financeiras.
- **Disponibilidade (Availability)**: O sistema deverá ser altamente disponível, com tempo de inatividade mínimo.
- **Usabilidade (Usability)**: A interface deverá ser intuitiva, fácil de usar tanto para o usuário comum quanto para o administrador.
- **Escalabilidade (Scalability)**: O sistema deverá ser capaz de lidar com o aumento no número de usuários e transações.