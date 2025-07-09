# 💰 Financial Tracker

## 📋 Resumo do Projeto

O **Financial Tracker** é um aplicativo Flutter multiplataforma para **gestão de finanças pessoais**. Ele permite aos usuários registrar transações financeiras (receitas ou despesas) e fornece uma visão geral do status financeiro. A interface do aplicativo está em português e identifica a ferramenta como "Controle Financeiro". 

Os usuários podem:
- Adicionar transações com título, valor, data e tipo
- Visualizar uma lista dividida entre receitas e despesas
- Consultar estatísticas como total de receitas, total de despesas e saldo
- Utilizar filtros por período e visualizar dados via gráficos

---

## 🚀 Funcionalidades Principais

- **Gerenciamento de Transações**: Inserção via formulário modal com ID único, título, valor, data e tipo. Suporta exclusão por deslize com opção de desfazer via Snackbar.
- **Edição de Transações**: Ao clicar no ícone de lápis, o usuário pode alterar os dados de uma transação existente (valor, descrição, data e tipo) diretamente na interface.
- **Resumo e Gráficos**: Tela inicial com cartão de resumo (totais e saldo) e gráfico de pizza (proporção receitas/despesas).
- **Filtro por Data**: Filtros por "hoje", "esta semana", "este mês", "personalizado" e "todos", com chips interativos.
- **Estado Reativo**: Uso da lib `signals_flutter` para atualização automática da interface.
- **Temas e Localização**: Suporte a temas claro/escuro e formatação brasileira de datas e moeda (ex: `R$ 1.234,56`).

---

## 🧱 Estrutura e Componentes

Arquitetura em camadas com separação clara entre **UI**, **lógica de negócio** e **dados**.

### 📱 Frontend (Flutter Widgets) - `lib/ui`

- `HomeScreen`: Tela principal
  - `AppBar` com botão de filtro
  - `SummaryCarousel`: cartão de resumo + gráfico
  - `DateFilterTransactions`: painel de filtros
  - Botões de ação: Receitas e Despesas
  - `TransactionCardSheets`: abas de transações

### 📝 Formulário de Transação

- `TransactionForm`: campos validados
- Ao submeter, chama comando de salvar via controller e atualiza a UI
- Também suporta **modo de edição**, preenchendo automaticamente os campos com os dados da transação selecionada.

### 🧠 Controller

- `HomePageController`:
  - Lista reativa de transações
  - Cálculo de totais e saldo via sinais computados
  - Comandos: carregar, filtrar, adicionar, excluir, desfazer
  - Estado da UI (ex: visibilidade do filtro)

### 🧩 Domínio (Entidades e Use Cases)

- `TransactionEntity`: modelo com métodos utilitários
- Casos de uso:
  - `AddTransactionUseCase`
  - `DeleteTransactionUseCase`
  - `GetTransactionsByDateUseCase` (entre outros)
- Facade para facilitar injeção dos use cases

### 💾 Dados (Repositório e Serviços)

- `TransactionRepositoryImpl`: interface `TransactionRepositoryContract`
- `TransactionFakeServiceImpl`: simulação em memória com `faker_dart`
- Falhas simuladas para testes (`InvalidData`, `APIFailure`)
- Objetos `Failure` encapsulam erros com mensagens do `MessagesError`

### 🛠 Utilitários e Configuração

- `Formatter`: formata datas e valores (pt-BR)
- `DateFilterType`: enum de filtros com lógica de datas
- Injeção com `auto_injector` em `dependencies.dart`
- `Result`: tipo funcional para `Success` e `Error`

### 🌐 Plataforma

Compatível com Android, iOS, Web, macOS, Windows e Linux. Código nativo gerado automaticamente. Toda a lógica em Dart.

---

## ⚙️ Configuração e Dependências

**Dependências principais (pubspec.yaml):**

```yaml
dependencies:
  flutter:
  cupertino_icons:
  signals_flutter:
  auto_injector:
  fl_chart:
  faker_dart:
  intl:
  uuid:

dev_dependencies:
  flutter_test:
  flutter_lints:
```

**Passos para execução:**

1. Instale o Flutter.
2. Rode o comando:
   ```bash
   flutter pub get
   ```
3. Execute em qualquer plataforma (sem necessidade de banco de dados externo).

