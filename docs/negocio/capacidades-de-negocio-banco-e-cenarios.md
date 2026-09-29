# Capacidades de Negócio — Banco e Cenários

## 1. Objetivo

Este documento identifica e organiza as **Capacidades de Negócio** relevantes para o case, primeiro em uma visão geral do banco e depois nos dois cenários avaliados:

- Cenário 1 — Conta de Pagamentos;
- Cenário 2 — Cashback com Parcerias.

A capacidade representa **o que o negócio é capaz de fazer**, independentemente de como isso será implementado tecnologicamente.

Portanto:

```text
Capability ≠ Functionalidade ≠ Microservice
```

A capacidade deve ser estável em relação à implementação e servir como ponte entre a estratégia e a arquitetura.

---

# 2. Base do Case

O case informa que:

- o banco possui portfólio predominantemente baseado em produtos de crédito;
- são citados Crédito Direto ao Consumidor, Cartão de Crédito, Crédito Pessoal, Consignado e Empréstimos com garantia;
- as capacidades foram construídas em silos;
- existe pouco reaproveitamento;
- o legado impacta a cadeia de valor;
- o banco busca ampliar o portfólio e aumentar o engajamento;
- Conta de Pagamentos e Cashback com parcerias apresentaram bons resultados nos testes;
- o novo produto deve contribuir para melhorar a arquitetura e acelerar lançamentos;
- o estilo arquitetural atual é Microservices e deve ser preservado;
- a análise deve considerar arquitetura TO-BE e plano de migração para elementos não aderentes.

Esses pontos são a base para o mapa de capacidades.

---

# 3. Mapa de Capacidades — Visão Geral

Uma primeira decomposição estratégica:

```mermaid
flowchart TB

    BANK["Banco"]

    BANK --> CUSTOMER["Gestão de Clientes"]
    BANK --> PRODUCT["Gestão de Produtos"]
    BANK --> CREDIT["Gestão de Crédito"]
    BANK --> ACCOUNT["Gestão de Contas"]
    BANK --> TRANSACTION["Gestão de Transações"]
    BANK --> BENEFITS["Gestão de Benefícios"]
    BANK --> PARTNER["Gestão de Parceiros"]
    BANK --> COMPLIANCE["Gestão de Controles e Compliance"]
    BANK --> INTEGRATION["Gestão de Integrações"]
```

Esta é uma visão de primeiro nível. A decomposição abaixo é uma hipótese de trabalho e deve ser refinada conforme os processos e limites de negócio forem detalhados.

---

# 4. Classificação das Capacidades

Para apoiar a análise estratégica, as capacidades podem ser classificadas inicialmente em:

- **Core** — capacidade potencialmente relacionada à diferenciação competitiva e à estratégia do negócio.
- **Supporting** — capacidade necessária ao negócio, mas que não representa necessariamente diferenciação.
- **Generic** — capacidade comum, padronizável ou potencialmente adquirível como commodity.

A classificação abaixo é **inicial**. O case não fornece informação suficiente para fechar definitivamente todas as classificações.

| ID | Capacidade | Classificação inicial | Justificativa |
|---|---|---|---|
| CAP-001 | Gestão de Clientes | Supporting | Necessária para diversos produtos e jornadas. |
| CAP-002 | Gestão de Produtos | Supporting | Suporta composição e administração do portfólio. |
| CAP-003 | Gestão de Crédito | Core / existente | Representa o principal domínio do portfólio atual. |
| CAP-004 | Gestão de Contas | A avaliar | Torna-se relevante para o cenário de Conta de Pagamentos. |
| CAP-005 | Gestão de Transações | Supporting / a avaliar | Capacidade transversal potencialmente reutilizável. |
| CAP-006 | Gestão de Benefícios | A avaliar | Surge como capacidade relevante no cenário de Cashback. |
| CAP-007 | Gestão de Parceiros | Supporting / a avaliar | Necessária para o ecossistema de Cashback. |
| CAP-008 | Controles e Compliance | Generic / Supporting | Capacidade necessária ao setor bancário. |
| CAP-009 | Gestão de Integrações | Generic / Supporting | Capacidade transversal de interoperabilidade. |

A classificação deverá ser revisitada após o levantamento de valor, diferenciação e estratégia do banco.

---

# 5. Decomposição das Capacidades

## 5.1 Gestão de Clientes

```mermaid
flowchart TB
    C["Gestão de Clientes"]

    C --> C1["Identificação de Cliente"]
    C --> C2["Cadastro de Cliente"]
    C --> C3["Manutenção de Dados"]
    C --> C4["Relacionamento com Produtos"]
    C --> C5["Consulta de Dados"]
```

### Papel

Permitir que o banco mantenha e disponibilize informações necessárias sobre seus clientes.

### Reuso

Alta possibilidade de reutilização entre os dois cenários.

---

# 6. Gestão de Produtos

```mermaid
flowchart TB
    P["Gestão de Produtos"]

    P --> P1["Definição de Produto"]
    P --> P2["Configuração de Produto"]
    P --> P3["Gestão do Ciclo de Vida"]
    P --> P4["Parametrização"]
    P --> P5["Composição de Oferta"]
```

### Papel

Representar a capacidade do banco de estruturar e administrar seu portfólio.

### Reuso

Pode ser utilizada tanto pela Conta de Pagamentos quanto pelo Cashback.

---

# 7. Gestão de Crédito

O case informa que o portfólio atual possui forte concentração em crédito.

```mermaid
flowchart TB
    C["Gestão de Crédito"]

    C --> C1["Crédito Direto ao Consumidor"]
    C --> C2["Cartão de Crédito"]
    C --> C3["Crédito Pessoal"]
    C --> C4["Consignado"]
    C --> C5["Empréstimos com Garantia"]
```

Neste momento, esses itens devem ser tratados como capacidades/produtos candidatos à decomposição, e não necessariamente como Bounded Contexts definitivos.

### Ponto arquitetural

O principal problema informado pelo case não é a existência dos produtos de crédito, mas o fato de suas capacidades terem sido construídas em silos e com pouco reaproveitamento.

---

# 8. Gestão de Contas

Capacidade especialmente relevante para o cenário de Conta de Pagamentos.

```mermaid
flowchart TB
    A["Gestão de Contas"]

    A --> A1["Abertura de Conta"]
    A --> A2["Manutenção de Conta"]
    A --> A3["Alteração de Status"]
    A --> A4["Bloqueio / Desbloqueio"]
    A --> A5["Encerramento de Conta"]
    A --> A6["Consulta de Conta"]
```

### Cenário relacionado

Conta de Pagamentos.

### Questão em aberto

O case não informa quais capacidades de conta já existem no banco. Portanto, não podemos afirmar que toda essa capacidade precisará ser construída.

---

# 9. Gestão de Transações

```mermaid
flowchart TB
    T["Gestão de Transações"]

    T --> T1["Recebimento de Transação"]
    T --> T2["Validação de Transação"]
    T --> T3["Processamento"]
    T --> T4["Registro"]
    T --> T5["Consulta"]
    T --> T6["Atualização de Estado"]
```

### Papel

Capacidade transversal potencialmente utilizada pelos dois cenários.

### Conta de Pagamentos

A transação representa uma operação sobre a conta.

### Cashback

A transação pode ser uma fonte de informação utilizada para determinar elegibilidade e calcular o benefício.

Essa diferença é importante:

```text
Conta de Pagamentos:
Account → Transaction

Cashback:
Transaction → Cashback
```

O sentido acima representa relação de negócio, não necessariamente dependência tecnológica.

---

# 10. Gestão de Benefícios

Capacidade específica que emerge com maior força no cenário de Cashback.

```mermaid
flowchart TB
    B["Gestão de Benefícios"]

    B --> B1["Definição de Benefício"]
    B --> B2["Elegibilidade"]
    B --> B3["Aplicação de Regras"]
    B --> B4["Cálculo"]
    B --> B5["Concessão"]
    B --> B6["Registro"]
    B --> B7["Consulta de Benefício"]
```

### Cenário relacionado

Cashback com Parcerias.

### Observação

O termo “Cashback” é tratado como uma forma específica de benefício dentro deste modelo. Essa definição deve ser validada com o negócio.

---

# 11. Gestão de Parceiros

```mermaid
flowchart TB
    P["Gestão de Parceiros"]

    P --> P1["Cadastro de Parceiro"]
    P --> P2["Manutenção de Parceiro"]
    P --> P3["Gestão de Acordos"]
    P --> P4["Configuração de Participação"]
    P --> P5["Gestão de Status"]
    P --> P6["Integração com Parceiro"]
```

### Cenário relacionado

Cashback com Parcerias.

### Questão em aberto

O case informa que o programa possui parcerias, mas não define o modelo operacional ou comercial desses parceiros.

---

# 12. Controles e Compliance

```mermaid
flowchart TB
    C["Controles e Compliance"]

    C --> C1["Controles Operacionais"]
    C --> C2["Regras de Compliance"]
    C --> C3["Monitoramento"]
    C --> C4["Auditoria"]
```

O case não detalha os requisitos regulatórios. Portanto, esta decomposição é apenas estrutural e deverá ser aprofundada posteriormente.

---

# 13. Gestão de Integrações

```mermaid
flowchart TB
    I["Gestão de Integrações"]

    I --> I1["Integração Interna"]
    I --> I2["Integração com Legado"]
    I --> I3["Integração com Core Bancário"]
    I --> I4["Integração com Parceiros"]
    I --> I5["Gestão de Contratos"]
```

Essa capacidade é especialmente relevante devido ao impacto do legado e à necessidade de interoperabilidade.

---

# 14. Capacidades — Cenário 1: Conta de Pagamentos

```mermaid
flowchart TB

    CP["Conta de Pagamentos"]

    CP --> C1["Gestão de Contas"]
    CP --> C2["Gestão de Clientes"]
    CP --> C3["Gestão de Transações"]
    CP --> C4["Gestão de Produtos"]
    CP --> C5["Controles e Compliance"]
    CP --> C6["Gestão de Integrações"]

    C1 --> C11["Abertura"]
    C1 --> C12["Manutenção"]
    C1 --> C13["Encerramento"]

    C3 --> C31["Movimentação"]
    C3 --> C32["Saldo"]
    C3 --> C33["Extrato"]
```

## Capacidades principais

| Capacidade | Importância no cenário |
|---|---|
| Gestão de Contas | Central |
| Gestão de Transações | Central |
| Gestão de Clientes | Necessária |
| Gestão de Produtos | Necessária |
| Controles e Compliance | Necessária |
| Gestão de Integrações | Necessária |

## Mapa de dependências conceituais

```text
Gestão de Clientes
        ↓
Gestão de Contas
        ↓
Gestão de Transações
        ↓
Controles / Compliance

Gestão de Produtos
        ↓
Gestão de Contas

Gestão de Integrações
        ↕
Todos os contextos necessários
```

---

# 15. Capacidades — Cenário 2: Cashback com Parcerias

```mermaid
flowchart TB

    CB["Cashback + Parcerias"]

    CB --> C1["Gestão de Benefícios"]
    CB --> C2["Gestão de Regras"]
    CB --> C3["Gestão de Elegibilidade"]
    CB --> C4["Gestão de Parceiros"]
    CB --> C5["Gestão de Transações"]
    CB --> C6["Gestão de Clientes"]
    CB --> C7["Gestão de Produtos"]
    CB --> C8["Controles e Compliance"]
    CB --> C9["Gestão de Integrações"]

    C1 --> C11["Concessão"]
    C1 --> C12["Registro"]

    C2 --> C21["Configuração"]

    C3 --> C31["Avaliação"]

    C4 --> C41["Cadastro"]
    C4 --> C42["Acordos"]
    C4 --> C43["Integração"]
```

## Capacidades principais

| Capacidade | Importância no cenário |
|---|---|
| Gestão de Benefícios | Central |
| Gestão de Regras | Central |
| Gestão de Elegibilidade | Central |
| Gestão de Parceiros | Central |
| Gestão de Transações | Necessária |
| Gestão de Clientes | Necessária |
| Gestão de Produtos | Necessária |
| Controles e Compliance | Necessária |
| Gestão de Integrações | Central |

---

# 16. Comparação das Capacidades

```mermaid
flowchart LR

    COMMON["Capacidades Compartilhadas"]

    COMMON --> CUSTOMER["Customer"]
    COMMON --> PRODUCT["Product"]
    COMMON --> TRANSACTION["Transaction"]
    COMMON --> COMPLIANCE["Compliance"]
    COMMON --> INTEGRATION["Integration"]

    CP["Conta de Pagamentos"]
    CB["Cashback"]

    CP --> ACCOUNT["Account"]

    CB --> BENEFITS["Benefits"]
    CB --> RULES["Rules"]
    CB --> ELIGIBILITY["Eligibility"]
    CB --> PARTNER["Partner"]
```

A visão evidencia uma possível área de reutilização:

```text
                 ┌── Conta de Pagamentos
                 │
Customer ────────┤
Product ─────────┤
Transaction ─────┤
Compliance ──────┤
Integration ─────┘

                 ┌── Cashback
                 │
Customer ────────┤
Product ─────────┤
Transaction ─────┤
Compliance ──────┤
Integration ─────┘
```

As capacidades específicas aparecem em pontos diferentes:

```text
Conta de Pagamentos
        ↓
Gestão de Contas

Cashback
        ↓
Gestão de Benefícios
Gestão de Regras
Gestão de Elegibilidade
Gestão de Parceiros
```

---

# 17. Matriz de Reutilização

| Capacidade | Conta de Pagamentos | Cashback | Potencial de Reuso |
|---|---:|---:|---|
| Gestão de Clientes | ✓ | ✓ | Alto |
| Gestão de Produtos | ✓ | ✓ | Alto |
| Gestão de Transações | ✓ | ✓ | Alto |
| Controles e Compliance | ✓ | ✓ | Alto |
| Gestão de Integrações | ✓ | ✓ | Alto |
| Gestão de Contas | ✓ | — | Específico |
| Gestão de Benefícios | — | ✓ | Específico |
| Gestão de Regras | — | ✓ | Específico |
| Gestão de Elegibilidade | — | ✓ | Específico |
| Gestão de Parceiros | — | ✓ | Específico |

---

# 18. Capacidades versus Bounded Contexts

A relação não deve ser 1:1.

```mermaid
flowchart LR

    CAP["Capability"]

    CAP --> ACCOUNT["Account Context"]
    CAP --> TRANSACTION["Transaction Context"]
    CAP --> CUSTOMER["Customer Context"]
    CAP --> PRODUCT["Product Context"]
    CAP --> BENEFITS["Benefits Context"]
    CAP --> PARTNER["Partner Context"]
```

Uma capacidade pode ser suportada por mais de um elemento tecnológico.

Da mesma forma, um Bounded Context pode suportar várias capacidades relacionadas.

Por isso, a sequência recomendada é:

```text
Capability
     ↓
Business Functions
     ↓
Bounded Context
     ↓
Application Components
     ↓
Microservices
```

---

# 19. Capacidades e Core Bancário

A pergunta sobre aquisição de Core Bancário deve ser tratada no nível de capacidades.

A análise deverá responder:

```mermaid
flowchart TB

    CORE["Core Bancário"]

    CORE --> Q1["Quais capacidades fornece?"]
    CORE --> Q2["Quais capacidades não fornece?"]
    CORE --> Q3["Quais capacidades devem permanecer no banco?"]
    CORE --> Q4["Quais capacidades serão integradas?"]
    CORE --> Q5["Qual impacto no legado?"]
    CORE --> Q6["Qual impacto no TO-BE?"]
```

Para o cenário de Conta de Pagamentos, a análise deve principalmente investigar sua relação com:

- Gestão de Contas;
- Gestão de Transações;
- capacidades bancárias relacionadas.

Para Cashback, a análise deve investigar principalmente se o Core oferece capacidades relevantes para:

- transações;
- clientes;
- produtos;
- integração;
- demais capacidades que possam ser necessárias.

Não é possível concluir, a partir do case isoladamente, quais capacidades uma plataforma específica de Core Bancário forneceria.

---

# 20. Capability Map Consolidado

```mermaid
quadrantChart
    title Capability Map — Visão Inicial
    x-axis "Baixa diferenciação" --> "Alta diferenciação"
    y-axis "Baixa relevância" --> "Alta relevância"

    "Gestão de Clientes": [0.35, 0.80]
    "Gestão de Produtos": [0.50, 0.75]
    "Gestão de Crédito": [0.80, 0.90]
    "Gestão de Contas": [0.70, 0.85]
    "Gestão de Transações": [0.55, 0.90]
    "Gestão de Benefícios": [0.75, 0.80]
    "Gestão de Parceiros": [0.65, 0.65]
    "Compliance": [0.25, 0.85]
    "Integrações": [0.30, 0.80]
```

> Os valores do gráfico acima são **posicionamentos ilustrativos**, não avaliações quantitativas derivadas do case. Para uma classificação formal, será necessário definir critérios de diferenciação e relevância com o negócio.

---

# 21. Rastreabilidade Estratégica

## Conta de Pagamentos

```text
Driver:
Aumentar portfólio
        ↓
Goal:
Expandir oferta
        ↓
Objective:
Habilitar Conta de Pagamentos
        ↓
Capability:
Gestão de Contas
        ↓
Capability:
Gestão de Transações
        ↓
Value Stream:
Disponibilizar / Utilizar Conta
```

## Cashback

```text
Driver:
Aumentar portfólio e engajamento
        ↓
Goal:
Expandir relacionamento
        ↓
Objective:
Habilitar Cashback
        ↓
Capability:
Gestão de Benefícios
        ↓
Capability:
Gestão de Regras
        ↓
Capability:
Gestão de Parceiros
        ↓
Value Stream:
Transacionar → Avaliar → Calcular → Conceder
```

---

# 22. Próximos passos

O mapa de capacidades deve ser utilizado como entrada para:

```text
Capability Map
      ↓
Capability Assessment
      ↓
Heatmap de Capacidades
      ↓
Value Streams
      ↓
Business Functions
      ↓
Bounded Contexts
      ↓
Building Blocks
      ↓
Application Architecture
      ↓
Microservices
```

A próxima etapa recomendada é realizar o **Capability Assessment**, classificando cada capacidade por:

- importância estratégica;
- maturidade atual;
- nível de reutilização;
- grau de silificação;
- impacto do legado;
- potencial de diferenciação;
- necessidade de transformação.

Isso permitirá identificar onde a arquitetura atual possui os maiores gaps e quais capacidades devem ser priorizadas na arquitetura TO-BE.
