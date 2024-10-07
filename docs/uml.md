## Diagrama UML

Nesta seção, apresentamos os diagramas UML do sistema, que ajudam a visualizar a estrutura e o relacionamento entre as principais entidades. O diagrama inclui classes como `User`, `Admin`, `Account`, `CheckingAccount`, `SavingsAccount` e `Transaction`, detalhando seus atributos e métodos, além das associações e heranças entre elas.

## Links para a documentação

- [README](../README.md)
- [Requisitos do Sistema](docs/requisitos.md)
- [Diagramas UML](docs/uml.md)
- [Documentação da API](docs/api_documentacao.md)
- [Arquitetura do Sistema](docs/arquitetura.md)
- [Plano de Testes](docs/plano_de_testes.md)

### User
- **Atributos**: name, email, listOfAccounts
- **Métodos**: createAccount(), viewAccounts(), deleteAccount()

### Admin
- **Herdado de**: User
- **Atributos/Métodos**: permissions (CRUD users and accounts), generateReports()

### Account (Interface)
- **Métodos**: withdraw(), deposit(), transfer()

### CheckingAccount (Conta Corrente)
- **Implementa**: Account
- **Atributos**: withdrawalLimit, maintenanceFee

### SavingsAccount (Conta Poupança)
- **Implementa**: Account
- **Atributos**: interestRate

### Transaction
- **Atributos**: date, value, type (withdrawal, deposit, transfer), originAccount, destinationAccount

### Associações e Heranças
- User tem muitos Account.
- Admin é uma herança de User.
- CheckingAccount e SavingsAccount implementam Account.
- Transaction está associada às contas (origin e destination).