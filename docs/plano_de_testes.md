## 5. Plano de Testes

O plano de testes descreve as estratégias e os casos de teste que serão implementados para garantir que o sistema funcione conforme o esperado. Os testes incluirão inicialmente testes manuais, com a intenção de incorporar testes automatizados ao longo do tempo.

## Links para a documentação

- [README](../README.md)
- [Requisitos do Sistema](docs/requisitos.md)
- [Diagramas UML](docs/uml.md)
- [Documentação da API](docs/api_documentacao.md)
- [Arquitetura do Sistema](docs/arquitetura.md)
- [Plano de Testes](docs/plano_de_testes.md)

### Seções principais:
- **Casos de Teste**
- **Testes de Integração**
- **Testes de Performance**

### Casos de Teste

1. **Adicionar nova conta corrente**
   - **Pré-condição**: Usuário autenticado.
   - **Passos**:
     1. Navegar para a página de criação de conta.
     2. Selecionar "Conta Corrente".
     3. Inserir dados válidos.
     4. Clicar em "Criar Conta".
   - **Resultado Esperado**: Conta criada com sucesso e mensagem de confirmação exibida.

2. **Visualizar contas existentes**
   - **Pré-condição**: Usuário autenticado.
   - **Passos**:
     1. Navegar para a página de visualização de contas.
   - **Resultado Esperado**: Lista de contas do usuário exibida corretamente com saldo e histórico.

3. **Excluir conta**
   - **Pré-condição**: Usuário autenticado com pelo menos uma conta.
   - **Passos**:
     1. Navegar para a página de contas.
     2. Selecionar uma conta.
     3. Clicar em "Excluir Conta".
   - **Resultado Esperado**: Conta excluída e notificação de sucesso exibida.

4. **Login de administrador**
   - **Pré-condição**: Usuário com permissões de administrador.
   - **Passos**:
     1. Acessar a página de login.
     2. Inserir credenciais de administrador.
     3. Clicar em "Entrar".
   - **Resultado Esperado**: Redirecionamento para o painel de administração.

### Testes de Integração

- **Teste de integração com MongoDB**
  - Verificar se todas as operações CRUD nas coleções de usuários e contas estão funcionando corretamente.
  - Realizar inserções, atualizações e deleções e verificar se os dados persistem e são recuperados corretamente.

- **Teste de comunicação entre front-end e back-end**
  - Testar todas as APIs com ferramentas como Postman ou Insomnia.
  - Verificar se as respostas estão no formato esperado e se os códigos de status HTTP estão corretos.

### Testes de Performance

- **Teste de carga**
  - Simular múltiplos usuários acessando o sistema simultaneamente.
  - Avaliar como o sistema se comporta sob carga elevada, observando tempos de resposta e possíveis falhas.

- **Teste de estresse**
  - Forçar o sistema além de seus limites normais para identificar pontos de falha e avaliar a recuperação.
