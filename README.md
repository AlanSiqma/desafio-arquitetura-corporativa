# Desafio de Arquitetura Corporativa

Repositório da análise de Enterprise Architecture para o desafio de arquitetura corporativa de um banco.

O trabalho parte do problema de negócio apresentado no case e evolui, de forma rastreável, até a decisão arquitetural, a arquitetura alvo, as arquiteturas intermediárias, os Building Blocks, a implementação e o planejamento de migração.

A abordagem utiliza principalmente TOGAF ADM, Business Architecture, Domain-Driven Design (DDD), Microservices, Value Stream / Value Chain, Architecture Decision Records (ADR) e princípios de evolução incremental.

---

## 1. Contexto do desafio

O banco possui um portfólio predominantemente relacionado a crédito, com capacidades construídas em silos e pouco reuso entre produtos.

O case apresenta dois produtos que tiveram bom desempenho nos testes:

- Conta de Pagamentos;
- Cashback com Parcerias.

A organização também questiona se a aquisição de uma plataforma de Core Banking poderia resolver parte dos problemas atuais.

A arquitetura existente utiliza **Microservices**, e a Architecture Vision deve preservar esse estilo arquitetural.

O desafio exige conectar problemas de negócio, capacidades, requisitos, funcionalidades, arquitetura atual, arquitetura alvo, arquiteturas intermediárias, Building Blocks, Value Chain / Value Stream e plano de migração.

---

## 2. Problema arquitetural

A análise identificou quatro grandes pontos estruturais no cenário atual:

```text
Capacidades em silos
        ↓
Baixo reuso
        ↓
Dependência / impacto do legado
        ↓
Dificuldade de evolução e lançamento de novos produtos
```

No cenário escolhido, também aparecem dois pontos específicos:

```text
Regras de Cashback acopladas ao produto
        +
Integrações heterogêneas com parceiros
```

O problema arquitetural, portanto, não é somente criar um novo produto.

A transformação precisa utilizar o novo produto como oportunidade para reduzir os estrangulamentos existentes sem reproduzir o padrão de silos.

---

## 3. Decisão arquitetural

Foram analisados dois cenários:

### Conta de Pagamentos

Possui forte relevância arquitetural por introduzir capacidades como:

- Gestão de Contas;
- Gestão de Transações;
- saldo;
- movimentação;
- relacionamento com Cliente e Produto;
- integração com capacidades bancárias existentes.

Também possui maior proximidade conceitual com capacidades que poderiam ser afetadas por uma futura decisão de Core Banking.

### Cashback com Parcerias

Introduz:

- Gestão de Benefícios;
- Regras;
- Elegibilidade;
- Gestão de Parceiros;
- concessão de benefícios;
- integração com Transações;
- integração com parceiros.

O cenário também permite reutilizar capacidades existentes de Cliente, Produto e Transação.

### Decisão registrada

A **ADR-002** estabelece:

> **Cashback com Parcerias é adotado como primeiro cenário de transformação arquitetural.**

A decisão não afirma que Cashback possui maior valor comercial.

O racional é utilizar Cashback como primeiro veículo de transformação para atacar os estrangulamentos arquiteturais identificados.

A decisão de aquisição de Core Banking permanece independente e deverá ser tratada posteriormente por uma análise de **Capability Fit/Gap**.

- [ADR-001 — Avaliação dos Cenários](docs/adr/ADR-001-cenarios-conta-pagamentos-cashback.md)
- [ADR-002 — Decisão do Cenário](docs/adr/ADR-002-decisao-cenario-transformacao-arquitetural.md)
- [Banca de Arquitetura](docs/banca-arquitetura-ia/banca-arquitetura-cenarios.md)

---

## 4. Linha de raciocínio arquitetural

A solução foi construída seguindo esta cadeia de decisão:

```text
Problema de negócio
        ↓
Drivers e objetivos
        ↓
Capacidades
        ↓
Value Stream / Value Chain
        ↓
Requisitos
        ↓
AS-IS
        ↓
Avaliação dos cenários
        ↓
Trade-offs
        ↓
ADR-002
        ↓
Cashback + Parcerias
        ↓
Estrangulamentos
        ↓
TO-BE
        ↓
Arquiteturas Intermediárias
        ↓
Building Blocks
        ↓
Implementation Architecture
        ↓
Migration Plan
        ↓
Implementation Governance
```

Essa sequência é a principal linha de rastreabilidade do repositório.

---

# 5. TOGAF ADM

A organização dos artefatos utiliza o TOGAF ADM como referência para a evolução arquitetural.

```text
Preliminary / Principles
        ↓
Phase A — Architecture Vision
        ↓
Phase B — Business Architecture
        ↓
Phase C — Information Systems Architecture
        ↓
Phase D — Technology Architecture
        ↓
Phase E — Opportunities & Solutions
        ↓
Phase F — Migration Planning
        ↓
Phase G — Implementation Governance
        ↓
Phase H — Architecture Change Management
```

Nem todos os artefatos representam uma fase isolada do ADM. Alguns são entradas, análises ou decisões que alimentam mais de uma fase.

### Fase A — Architecture Vision / Strategy & Motivation

Os documentos de Strategy & Motivation registram:

- stakeholders;
- drivers;
- assessment;
- goals;
- objectives;
- outcomes;
- capabilities estratégicas;
- Value Streams;
- hipóteses arquiteturais;
- questões em aberto.

- [Strategy & Motivation — Conta de Pagamentos](docs/TOGAF/01-Strategy%20%26%20Motivation/strategy-motivation-cenario-1-conta-pagamentos.md)
- [Strategy & Motivation — Cashback](docs/TOGAF/01-Strategy%20%26%20Motivation/strategy-motivation-cenario-2-cashback.md)

### Fase B — Business Architecture

A Business Architecture detalha:

- Value Chain;
- Value Stream × Value Chain;
- capacidades;
- Business Functions;
- Business Services;
- processos de negócio;
- objetos de negócio;
- interoperabilidade;
- impacto do legado;
- gaps;
- oportunidades;
- reuso.

- [Business Architecture — Conta de Pagamentos](docs/TOGAF/02-Business%20Architecture/business-architecture-conta-pagamentos.md)
- [Business Architecture — Cashback com Parcerias](docs/TOGAF/02-Business%20Architecture/business-architecture-cashback-parcerias.md)

### Fases C/D — Information Systems / Technology

Os artefatos de domínio, contexto e arquitetura fornecem a base para a evolução da arquitetura de sistemas e tecnologia:

- Bounded Contexts;
- Context Maps;
- capacidades;
- Building Blocks;
- integração;
- Microservices;
- APIs;
- eventos;
- isolamento do legado.

O detalhamento tecnológico permanece deliberadamente em nível arquitetural, pois o case não fornece inventário tecnológico, volumes, SLAs ou topologia de infraestrutura.

### Fase E — Opportunities & Solutions

A Fase E materializa as oportunidades e soluções:

- TO-BE;
- arquiteturas intermediárias;
- Building Blocks;
- Solution Building Blocks;
- Work Packages;
- abordagem de implementação.

- [Estrangulamentos, TO-BE e Arquitetura Intermediária](docs/arquitetura/estrangulamentos-to-be-arquitetura-intermediaria.md)
- [Building Blocks — Cashback com Parcerias](docs/arquitetura/building-blocks-cashback-parcerias.md)
- [Implementation Architecture](docs/TOGAF/05-Implementation%20%26%20Migration/implementation-architecture-togaf.md)

### Fase F — Migration Planning

A Fase F transforma as arquiteturas de transição em uma estratégia de migração:

- Transition Architectures;
- Work Packages;
- dependências;
- roadmap;
- riscos;
- critérios de transição;
- estratégia de coexistência;
- redução progressiva da dependência do legado.

- [Migration Plan](docs/TOGAF/05-Implementation%20%26%20Migration/migration-plan-togaf.md)

### Fase G — Implementation Governance

A Implementation Architecture também estabelece mecanismos de governança:

- Architecture Compliance Reviews;
- Architecture Gates;
- contratos arquiteturais;
- validação de aderência;
- governança da implementação.

### Fase H — Architecture Change Management

A evolução não termina no TO-BE.

Mudanças relevantes — novos produtos, parceiros, requisitos, regulações, plataformas ou alterações significativas no legado — podem iniciar novos ciclos de avaliação arquitetural.

---

# 6. Arquitetura AS-IS

O AS-IS representa o conhecimento arquitetural disponível no case.

O documento distingue fatos fornecidos pelo case de hipóteses arquiteturais necessárias para representar o cenário.

Principais características:

- portfólio predominantemente baseado em crédito;
- capacidades em silos;
- pouco reuso;
- impacto do legado na cadeia de valor;
- dificuldade de evolução;
- arquitetura baseada em Microservices.

- [Arquitetura Atual — AS-IS](docs/arquitetura/arquitetura-atual-as-is.md)

---

# 7. Estrangulamentos

A escolha de Cashback permite atacar os estrangulamentos sem exigir uma transformação Big Bang.

Os principais estrangulamentos identificados são:

| Estrangulamento | Resposta arquitetural |
|---|---|
| Capacidades em silos | Building Blocks reutilizáveis |
| Baixo reuso | Reutilização de Customer, Product e Transaction |
| Dependência do legado | ACL / Adapter e coexistência |
| Integrações pouco explícitas | APIs, eventos e contratos |
| Regras acopladas | Rules e Eligibility explícitos |
| Parceiros heterogêneos | Partner Management + Adapters |

- [Estrangulamentos, TO-BE e Arquitetura Intermediária](docs/arquitetura/estrangulamentos-to-be-arquitetura-intermediaria.md)

---

# 8. TO-BE e Arquiteturas Intermediárias

O princípio central da evolução é:

```text
AS-IS
  ↓
Arquitetura Intermediária
  ↓
Arquitetura Intermediária
  ↓
Arquitetura Intermediária
  ↓
TO-BE
```

O **TO-BE** representa o estado arquitetural desejado.

A **Arquitetura Intermediária** representa os estados de coexistência necessários para atravessar os estrangulamentos.

A evolução proposta é:

```text
TA-1 — Isolamento
        ↓
TA-2 — Benefits + Rules
        ↓
TA-3 — Eligibility + Partner
        ↓
TA-4 — Consolidação
        ↓
TO-BE
```

Essa abordagem evita exigir a substituição imediata do legado.

---

# 9. Building Blocks

Os Building Blocks foram derivados dos estrangulamentos e da arquitetura alvo.

### Capacidades reutilizáveis

- Customer Management;
- Product Management;
- Transaction Management;
- Compliance.

### Cashback

- Benefits Management;
- Cashback Rules;
- Eligibility Management;
- Benefit Granting.

### Parceiros

- Partner Management;
- Partner Integration Adapter.

### Integração e transição

- API Layer;
- Event Integration;
- Legacy Adapter / ACL.

Um Building Block **não é automaticamente um Microservice**.

A decomposição em Microservices deve ser derivada posteriormente a partir de:

- Bounded Contexts;
- coesão;
- autonomia;
- ownership dos dados;
- consistência;
- evolução;
- dependências;
- contratos.

- [Building Blocks — Cashback com Parcerias](docs/arquitetura/building-blocks-cashback-parcerias.md)

---

# 10. DDD

A análise utiliza DDD para ajudar a definir limites de domínio e relações entre contextos.

### Contextos gerais identificados

- Customer Management;
- Product Management;
- Credit;
- Account;
- Transaction;
- Benefits;
- Partner Management;
- Compliance;
- Integration.

### No cenário Cashback

Os principais contextos candidatos são:

```text
Customer
Product
Transaction
       │
       ▼
Benefits / Cashback
   ├── Rules
   ├── Eligibility
   └── Granting

Partner
   │
   ▼
Partner Integration
```

Os Bounded Contexts não devem ser confundidos com Microservices.

- [Bounded Contexts — Geral e Cenários](docs/dominio/bounded-contexts-geral-e-cenarios.md)
- [Context Map — AS-IS e Cenários](docs/dominio/context-map-as-is-e-cenarios.md)
- [Linguagem Ubíqua](docs/dominio/linguagem-ubiqua.md)

---

# 11. Requisitos

Os requisitos foram mantidos separados em funcionais e não funcionais.

### Funcionais

Cobrem, entre outros:

- Conta de Pagamentos;
- Cashback;
- parceiros;
- regras;
- cálculo;
- registro;
- integração;
- interoperabilidade;
- reuso.

- [Requisitos Funcionais](docs/requisitos/requisitos-funcionais.md)

### Não funcionais

Cobrem, entre outros:

- preservação de Microservices;
- time-to-market;
- reuso;
- interoperabilidade;
- desacoplamento do legado;
- evolução TO-BE;
- migração;
- governança;
- aderência arquitetural.

O case não fornece métricas quantitativas suficientes para inventar requisitos de disponibilidade, latência, throughput, RTO, RPO ou volumes.

- [Requisitos Não Funcionais](docs/requisitos/requisitos-nao-funcionais.md)

---

# 12. Architecture Improvement Proposals

As AIPs registram propostas arquiteturais específicas para os dois cenários antes da decisão final.

- [AIP-001 — Conta de Pagamentos](docs/aip/AIP-001-conta-de-pagamentos.md)
- [AIP-002 — Cashback com Parcerias](docs/aip/AIP-002-cashback-parcerias.md)

A existência das duas AIPs não significa que os dois cenários foram adotados.

A decisão de transformação arquitetural está registrada na ADR-002.

---

# 13. ADRs

### ADR-001

Registra a avaliação inicial dos dois cenários e mantém a decisão em aberto naquela etapa.

- [ADR-001 — Cenários Conta de Pagamentos e Cashback](docs/adr/ADR-001-cenarios-conta-pagamentos-cashback.md)

### ADR-002

Registra a decisão posterior:

```text
Cashback + Parcerias
        ↓
Primeiro veículo de transformação arquitetural
```

A decisão:

- não afirma superioridade comercial do Cashback;
- não elimina Conta de Pagamentos;
- não aprova nem rejeita Core Banking;
- estabelece condições para evitar novo silo;
- direciona a arquitetura para evolução incremental.

- [ADR-002 — Decisão do Cenário para Transformação Arquitetural](docs/adr/ADR-002-decisao-cenario-transformacao-arquitetural.md)

---

# 14. Implementation e Migration

A implementação e a migração são tratadas de acordo com o ADM.

### Implementation Architecture

A implementação materializa:

- Solution Building Blocks;
- Work Packages;
- arquitetura de implementação;
- contratos;
- APIs;
- eventos;
- Microservices como estilo;
- Architecture Gates;
- Implementation Governance.

- [Implementation Architecture](docs/TOGAF/05-Implementation%20%26%20Migration/implementation-architecture-togaf.md)

### Migration Plan

O plano de migração materializa:

- Transition Architectures;
- Work Packages;
- dependências;
- roadmap;
- riscos;
- critérios de transição;
- governança;
- evolução até o TO-BE.

- [Migration Plan](docs/TOGAF/05-Implementation%20%26%20Migration/migration-plan-togaf.md)

---

# 15. Rastreabilidade

A arquitetura foi construída para permitir rastrear uma decisão até sua origem:

```text
Case
 ↓
Problema de negócio
 ↓
Driver
 ↓
Goal / Objective
 ↓
Capability
 ↓
Value Stream
 ↓
Requirement
 ↓
Estrangulamento
 ↓
Alternativas
 ↓
Trade-off
 ↓
ADR
 ↓
TO-BE
 ↓
Building Block
 ↓
Solution Building Block
 ↓
Work Package
 ↓
Migration
 ↓
Implementation Governance
```

A rastreabilidade também permite fazer o caminho inverso:

```text
Microservice / Component
        ↑
Building Block
        ↑
Capability
        ↑
Business Problem
```

---

# 16. Estrutura do repositório

```text
.
├── README.md
│
├── docs/
│   │
│   ├── requisitos/
│   │   ├── requisitos-funcionais.md
│   │   └── requisitos-nao-funcionais.md
│   │
│   ├── dominio/
│   │   ├── linguagem-ubiqua.md
│   │   ├── bounded-contexts-geral-e-cenarios.md
│   │   └── context-map-as-is-e-cenarios.md
│   │
│   ├── negocio/
│   │   └── capacidades-de-negocio-banco-e-cenarios.md
│   │
│   ├── adr/
│   │   ├── ADR-001-cenarios-conta-pagamentos-cashback.md
│   │   └── ADR-002-decisao-cenario-transformacao-arquitetural.md
│   │
│   ├── aip/
│   │   ├── AIP-001-conta-de-pagamentos.md
│   │   └── AIP-002-cashback-parcerias.md
│   │
│   ├── banca-arquitetura-ia/
│   │   └── banca-arquitetura-cenarios.md
│   │
│   ├── arquitetura/
│   │   ├── arquitetura-atual-as-is.md
│   │   ├── estrangulamentos-to-be-arquitetura-intermediaria.md
│   │   └── building-blocks-cashback-parcerias.md
│   │
│   └── TOGAF/
│       ├── 01-Strategy & Motivation/
│       │   ├── strategy-motivation-cenario-1-conta-pagamentos.md
│       │   └── strategy-motivation-cenario-2-cashback.md
│       │
│       ├── 02-Business Architecture/
│       │   ├── business-architecture-conta-pagamentos.md
│       │   └── business-architecture-cashback-parcerias.md
│       │
│       └── 05-Implementation & Migration/
│           ├── implementation-architecture-togaf.md
│           └── migration-plan-togaf.md
```

---

# 17. Mapa dos principais artefatos

| Artefato | Papel |
|---|---|
| Strategy & Motivation | Drivers, goals, objectives, outcomes e Value Streams |
| Business Architecture | Capacidades, Value Chain, funções, serviços e processos |
| AS-IS | Situação arquitetural atual conhecida |
| ADR-001 | Avaliação inicial dos cenários |
| AIP-001 / AIP-002 | Propostas arquiteturais dos cenários |
| Banca | Avaliação dos trade-offs e perspectivas arquiteturais |
| ADR-002 | Decisão do primeiro cenário de transformação |
| Estrangulamentos | Gaps e pontos de estrangulamento |
| TO-BE / Intermediárias | Estado alvo e estados de transição |
| Building Blocks | Capacidades/blocos necessários à solução |
| Bounded Contexts | Limites de domínio candidatos |
| Context Map | Relações entre contextos |
| Implementation Architecture | Fase E/G: solução e governança |
| Migration Plan | Fase F: transição e roadmap |

---

# 18. Princípios arquiteturais

### Preservar Microservices

O estilo arquitetural existente deve ser preservado.

### Reuso antes de duplicação

Capacidades existentes devem ser reutilizadas quando aderentes ao novo cenário.

### Não criar outro silo

Cashback deve utilizar capacidades compartilhadas e produzir capacidades potencialmente reutilizáveis.

### Isolar o legado

O legado pode coexistir durante a transição, mas não deve definir o modelo dos novos domínios.

### Contratos explícitos

As integrações devem possuir contratos claros.

### Evolução incremental

O caminho AS-IS → TO-BE deve utilizar arquiteturas intermediárias quando necessário.

### Domínio antes da decomposição

Bounded Contexts e responsabilidades de negócio devem orientar a decomposição em Microservices.

### Core Banking como decisão independente

A eventual aquisição de Core Banking deve ser avaliada por Capability Fit/Gap e não presumida como solução para o problema arquitetural.

---

# 19. Estado atual

O repositório já contém:

- requisitos;
- linguagem ubíqua;
- Strategy & Motivation;
- Business Architecture;
- AS-IS;
- Bounded Contexts;
- Context Maps;
- AIPs;
- ADR-001;
- banca arquitetural;
- ADR-002;
- estrangulamentos;
- TO-BE;
- arquiteturas intermediárias;
- Building Blocks;
- Implementation Architecture;
- Migration Plan.

A próxima evolução relevante não é adicionar mais documentos conceituais isolados, mas consolidar os artefatos existentes, validar a rastreabilidade e, se necessário, detalhar a arquitetura de sistemas e os contratos sem antecipar decisões que o case não suporta.

---

# 20. Resultado arquitetural

A solução pode ser resumida como:

```text
O banco precisa evoluir o portfólio
        ↓
Mas possui silos, baixo reuso e impacto do legado
        ↓
Dois cenários são avaliados
        ↓
Conta de Pagamentos × Cashback com Parcerias
        ↓
A banca avalia os trade-offs
        ↓
Cashback é escolhido como veículo de transformação
        ↓
Não por superioridade comercial,
mas por seu papel arquitetural
        ↓
Estrangulamentos são explicitados
        ↓
TO-BE é definido
        ↓
Arquiteturas intermediárias permitem a transição
        ↓
Building Blocks materializam as capacidades
        ↓
Implementation define a realização
        ↓
Migration define a trajetória
        ↓
Governança garante aderência
        ↓
Core Banking permanece como decisão independente
```

---

## Status

**Arquitetura em consolidação.**

A decisão arquitetural principal está registrada na ADR-002. Os artefatos posteriores detalham a evolução para TO-BE, arquiteturas intermediárias, Building Blocks, implementação e migração.
