# Scenario 2 — Cashback com Parcerias
# Strategy & Motivation Layer

## 1. Objetivo

Este documento representa a camada de **Strategy & Motivation** para o cenário de **Programa de Cashback com Parcerias**, utilizando os conceitos de arquitetura estratégica associados ao TOGAF e à modelagem de motivação/estratégia.

O objetivo é estabelecer a rastreabilidade entre:

```text
Drivers
   ↓
Assessment
   ↓
Problems / Issues
   ↓
Goals
   ↓
Objectives
   ↓
Outcomes
   ↓
Capabilities
   ↓
Value Streams
```

A camada não define ainda a arquitetura tecnológica TO-BE nem uma decisão sobre aquisição de Core Bancário.

---

# 2. Evidências do Case

O case apresenta os seguintes fatos relevantes para este cenário:

- O banco deseja aumentar o portfólio de produtos e o engajamento.
- Conta de Pagamentos e Cashback com parcerias foram os produtos que apresentaram melhores resultados nos testes realizados.
- O C-level entende que ambos os produtos endereçam o problema de engajamento, mas apenas um será priorizado.
- Existe a expectativa de que o novo produto também contribua para melhorar a arquitetura atual e acelerar o lançamento de novos produtos.
- O CTO questiona se a aquisição de uma plataforma de Core Bancário poderia resolver esses problemas.
- O portfólio atual é predominantemente baseado em produtos de crédito.
- As capacidades atuais foram construídas em silos, com pouco reaproveitamento.
- O legado impacta a cadeia de valor da companhia.
- A arquitetura atual utiliza Microservices e esse estilo deve ser preservado.
- A análise deve considerar boas práticas do setor bancário.
- Elementos não aderentes devem ser tratados em uma arquitetura TO-BE e em um plano de migração.

O case identifica explicitamente o Cashback como um programa com **parcerias**, portanto a análise deste cenário considera o relacionamento entre o banco, os clientes, as transações e os parceiros.

---

# 3. Stakeholders

```mermaid
flowchart LR
    CLEVEL["C-Level"]
    CIO["CIO"]
    CTO["CTO"]
    EA["Enterprise Architecture"]
    BUSINESS["Áreas de Negócio"]
    TECHNOLOGY["Tecnologia"]
    CUSTOMER["Cliente"]
    PARTNER["Parceiro"]

    CLEVEL -->|"Direcionamento estratégico"| EA
    CIO -->|"Solicita análise"| EA
    CTO -->|"Questão arquitetural"| EA
    BUSINESS -->|"Necessidades de negócio"| EA
    TECHNOLOGY -->|"Arquitetura atual"| EA
    CUSTOMER -->|"Utilização / Engajamento"| BUSINESS
    PARTNER -->|"Oferta / parceria"| BUSINESS

    EA -->|"Direcionamento arquitetural"| CLEVEL
    EA -->|"Direcionamento"| TECHNOLOGY
```

## 3.1 C-Level

Interesses:

- ampliar o portfólio;
- aumentar o engajamento;
- priorizar um novo produto;
- melhorar a arquitetura;
- acelerar novos lançamentos.

## 3.2 CIO

Interesse:

- garantir análise de Enterprise Architecture antes da decisão arquitetural.

## 3.3 CTO

Interesse:

- avaliar a hipótese de aquisição de uma plataforma de Core Bancário.

## 3.4 Enterprise Architecture

Responsabilidades no contexto do case:

- analisar os problemas;
- identificar capacidades;
- avaliar os cenários;
- analisar arquitetura atual;
- propor arquitetura alvo;
- avaliar alternativas arquiteturais.

## 3.5 Cliente

Interesse:

- receber benefícios;
- participar do programa;
- utilizar os produtos e parceiros elegíveis.

## 3.6 Parceiro

Interesse relacionado ao cenário:

- participar do programa;
- disponibilizar ofertas elegíveis;
- estabelecer regras comerciais com o banco.

O case não detalha o modelo comercial entre banco e parceiro. Esse ponto permanece como questão a ser validada.

---

# 4. Drivers Estratégicos

```mermaid
flowchart TB

    D1["Aumentar o portfólio de produtos"]
    D2["Aumentar o engajamento dos clientes"]
    D3["Acelerar lançamento de novos produtos"]
    D4["Melhorar a arquitetura atual"]
    D5["Reduzir impacto do legado na cadeia de valor"]
    D6["Aumentar reaproveitamento de capacidades"]

    G1["Expandir oferta de produtos"]
    G2["Aumentar relacionamento com clientes"]
    G3["Evoluir capacidade arquitetural"]
    G4["Aumentar reutilização e desacoplamento"]

    D1 --> G1
    D2 --> G2
    D3 --> G3
    D4 --> G3
    D5 --> G4
    D6 --> G4
```

| ID | Driver | Natureza |
|---|---|---|
| D-001 | Aumentar o portfólio de produtos | Negócio |
| D-002 | Aumentar o engajamento dos clientes | Negócio |
| D-003 | Acelerar o lançamento de novos produtos | Estratégico |
| D-004 | Melhorar a arquitetura atual | Arquitetural |
| D-005 | Reduzir o impacto do legado na cadeia de valor | Arquitetural |
| D-006 | Aumentar o reaproveitamento das capacidades | Arquitetural |

---

# 5. Assessment — Situação Atual

Os problemas apresentados pelo case são:

```mermaid
flowchart TB

    CURRENT["Situação Atual"]

    CURRENT --> P1["Capacidades construídas em silos"]
    CURRENT --> P2["Pouco reaproveitamento"]
    CURRENT --> P3["Legado impactando a cadeia de valor"]
    CURRENT --> P4["Portfólio concentrado em produtos de crédito"]
    CURRENT --> P5["Necessidade de acelerar novos produtos"]

    P1 --> IMP["Impacto arquitetural e de negócio"]
    P2 --> IMP
    P3 --> IMP
    P4 --> IMP
    P5 --> IMP
```

| ID | Problema | Evidência |
|---|---|---|
| P-001 | Capacidades construídas em silos | Case |
| P-002 | Baixo reaproveitamento de capacidades | Case |
| P-003 | Legado impactando a cadeia de valor | Case |
| P-004 | Portfólio predominantemente baseado em crédito | Case |
| P-005 | Necessidade de acelerar lançamentos | Case |

---

# 6. Goals — Objetivos Estratégicos

## G-001 — Expandir o portfólio

Disponibilizar um novo produto de relacionamento baseado em Cashback e parcerias.

## G-002 — Aumentar o engajamento

Utilizar o programa de Cashback como mecanismo de relacionamento entre o banco, clientes e parceiros.

O case afirma que o Cashback está entre os produtos que apresentaram bons resultados nos testes e que os produtos avaliados endereçam o problema de engajamento.

## G-003 — Acelerar o lançamento de novos produtos

Criar condições para que novas ofertas possam reutilizar capacidades e funcionalidades existentes.

## G-004 — Aumentar o reaproveitamento

Reduzir a construção isolada de capacidades e favorecer sua utilização por diferentes produtos.

## G-005 — Reduzir o impacto do legado

Criar uma evolução arquitetural que diminua a dependência dos novos produtos em relação aos silos existentes.

---

# 7. Objectives — Cenário Cashback

```mermaid
flowchart TB

    G1["Expandir portfólio"]
    G2["Aumentar engajamento"]
    G3["Acelerar lançamentos"]
    G4["Aumentar reuso"]
    G5["Reduzir impacto do legado"]

    O1["Habilitar Programa de Cashback"]
    O2["Criar capacidade de Gestão de Benefícios"]
    O3["Permitir gestão de parceiros"]
    O4["Permitir evolução das regras de Cashback"]
    O5["Reutilizar capacidades existentes"]
    O6["Desacoplar o programa dos produtos existentes"]

    G1 --> O1
    G2 --> O1

    G3 --> O2
    G4 --> O2
    G4 --> O3
    G4 --> O4
    G5 --> O6

    O1 --> O2
    O2 --> O4
    O2 --> O5
    O3 --> O5
    O4 --> O6
```

---

# 8. Outcomes

Os outcomes abaixo representam resultados esperados da transformação, não resultados já comprovados.

| ID | Outcome | Relação |
|---|---|---|
| OC-001 | Programa de Cashback disponível | O-001 |
| OC-002 | Capacidade de gestão de benefícios estabelecida | O-002 |
| OC-003 | Parceiros integrados ao programa | O-003 |
| OC-004 | Regras de Cashback evoluíveis | O-004 |
| OC-005 | Capacidades existentes reutilizadas | O-005 |
| OC-006 | Menor dependência direta do legado | O-006 |
| OC-007 | Capacidade de incorporar novos parceiros sem redesenhar todo o produto | O-003/O-004 |

O último outcome é uma hipótese arquitetural derivada da necessidade de trabalhar com parceiros e deve ser validado posteriormente.

---

# 9. Capabilities Estratégicas

Para o cenário de Cashback:

```mermaid
flowchart TB

    CAP["Capacidades necessárias"]

    CAP --> C1["Gestão de Benefícios"]
    CAP --> C2["Gestão de Regras"]
    CAP --> C3["Gestão de Elegibilidade"]
    CAP --> C4["Cálculo de Cashback"]
    CAP --> C5["Gestão de Parceiros"]
    CAP --> C6["Gestão de Transações"]
    CAP --> C7["Gestão de Clientes"]
    CAP --> C8["Gestão de Produtos"]
    CAP --> C9["Integração"]
    CAP --> C10["Controles e Compliance"]

    C1 --> C11["Registro de Benefícios"]
    C2 --> C21["Configuração de Regras"]
    C3 --> C31["Avaliação de Elegibilidade"]
    C4 --> C41["Cálculo do Benefício"]
    C5 --> C51["Cadastro de Parceiros"]
    C5 --> C52["Acordos"]
```

## Capacidades relevantes

| Capacidade | Papel no cenário |
|---|---|
| Gestão de Benefícios | Capacidade central do programa |
| Gestão de Regras | Determina as condições de concessão |
| Gestão de Elegibilidade | Determina se cliente/transação são elegíveis |
| Cálculo de Cashback | Determina o valor do benefício |
| Gestão de Parceiros | Administra participantes do ecossistema |
| Gestão de Transações | Fornece informações relevantes para avaliação |
| Gestão de Clientes | Identifica o cliente |
| Gestão de Produtos | Identifica produtos relacionados |
| Integração | Permite comunicação com sistemas internos e parceiros |
| Controles e Compliance | Suporta controles aplicáveis |

---

# 10. Value Stream

Um fluxo de valor candidato para o cenário é:

```mermaid
flowchart LR

    V1["Atrair Cliente"]
    V2["Disponibilizar Oferta"]
    V3["Realizar Transação"]
    V4["Avaliar Elegibilidade"]
    V5["Calcular Cashback"]
    V6["Conceder Benefício"]
    V7["Engajar Cliente"]

    V1 --> V2 --> V3 --> V4 --> V5 --> V6 --> V7
```

Em uma visão simplificada:

```text
Atrair
   ↓
Ofertar
   ↓
Transacionar
   ↓
Avaliar
   ↓
Calcular
   ↓
Conceder
   ↓
Engajar
```

Esse fluxo é uma hipótese inicial e deverá ser refinado com as regras reais do programa.

---

# 11. Ecossistema do Value Stream

O cenário possui uma característica adicional em relação à Conta de Pagamentos: a presença de parceiros.

```mermaid
flowchart LR

    CUSTOMER["Cliente"]
    BANK["Banco"]
    PARTNER["Parceiro"]

    CUSTOMER -->|"Participa"| BANK
    BANK -->|"Programa"| CUSTOMER

    PARTNER -->|"Oferta / Parceria"| BANK
    BANK -->|"Benefício / Relacionamento"| PARTNER

    CUSTOMER -->|"Transação"| PARTNER
    PARTNER -->|"Informação da transação"| BANK
```

O fluxo real de integração dependerá do modelo comercial e operacional definido para o programa.

O case não especifica como as transações dos parceiros serão disponibilizadas ao banco. Portanto, esse aspecto permanece em aberto.

---

# 12. Strategy & Motivation Consolidada

```mermaid
flowchart TB

    D1["Aumentar portfólio"]
    D2["Aumentar engajamento"]
    D3["Acelerar lançamentos"]
    D4["Melhorar arquitetura"]
    D5["Reduzir impacto do legado"]

    P1["Capacidades em silos"]
    P2["Pouco reaproveitamento"]
    P3["Legado impactando cadeia de valor"]

    G1["Expandir portfólio"]
    G2["Aumentar engajamento"]
    G3["Acelerar lançamentos"]
    G4["Aumentar reutilização"]
    G5["Reduzir dependência do legado"]

    O1["Habilitar Cashback"]
    O2["Gestão de Benefícios"]
    O3["Gestão de Parceiros"]
    O4["Regras evolutivas"]
    O5["Desacoplamento"]

    C1["Benefits"]
    C2["Rules"]
    C3["Eligibility"]
    C4["Partner Management"]
    C5["Transaction"]
    C6["Customer"]
    C7["Product"]

    D1 --> G1
    D2 --> G2
    D3 --> G3
    D4 --> G4
    D5 --> G5

    P1 --> G4
    P2 --> G4
    P3 --> G5

    G1 --> O1
    G2 --> O1
    G3 --> O2
    G3 --> O3
    G4 --> O2
    G4 --> O3
    G4 --> O4
    G5 --> O5

    O1 --> C1
    O2 --> C1
    O3 --> C4
    O4 --> C2
    O4 --> C3
    O5 --> C1
    O5 --> C4

    C5 --> C1
    C6 --> C1
    C7 --> C5
```

---

# 13. Relação com Bounded Contexts

Os Bounded Contexts identificados anteriormente podem ser associados às capacidades estratégicas:

```mermaid
flowchart LR

    BENEFITS["Benefits / Cashback Context"]
    PARTNER["Partner Management Context"]
    TRANSACTION["Transaction Context"]
    CUSTOMER["Customer Context"]
    PRODUCT["Product Context"]
    COMPLIANCE["Compliance Context"]

    BENEFITS --> C1["Gestão de Benefícios"]
    BENEFITS --> C2["Regras"]
    BENEFITS --> C3["Elegibilidade"]
    BENEFITS --> C4["Cálculo"]

    PARTNER --> C5["Gestão de Parceiros"]

    TRANSACTION --> C6["Gestão de Transações"]

    CUSTOMER --> C7["Gestão de Clientes"]

    PRODUCT --> C8["Gestão de Produtos"]

    COMPLIANCE --> C9["Controles"]
```

O `Benefits / Cashback Context` aparece como o principal contexto específico do cenário.

Isso não significa que ele já deva ser transformado diretamente em um único Microservice.

---

# 14. Relação com os Requisitos

| Requisito | Elemento estratégico |
|---|---|
| Disponibilizar programa de Cashback | Habilitar Cashback |
| Cadastro e gestão de parceiros | Gestão de Parceiros |
| Definir regras de Cashback | Gestão de Regras |
| Calcular Cashback | Cálculo de Cashback |
| Registrar Cashback | Gestão de Benefícios |
| Integrar com produtos existentes | Reutilização de capacidades |
| Integrar com parceiros | Gestão de Integrações |
| Permitir interoperabilidade | Evolução arquitetural |
| Manter Microservices | Restrição arquitetural |
| Acelerar lançamento de produtos | Objetivo estratégico |
| Reduzir dependência do legado | Objetivo arquitetural |

---

# 15. Hipóteses Arquiteturais

### H-001 — Contexto próprio para benefícios

O programa de Cashback deve possuir uma fronteira de negócio própria para evitar que suas regras sejam incorporadas diretamente aos produtos existentes.

### H-002 — Regras separadas dos produtos

As regras de elegibilidade e cálculo devem permanecer desacopladas dos produtos que originam as transações.

### H-003 — Parceiros possuem contexto próprio

As informações e responsabilidades relacionadas aos parceiros devem ser separadas das regras internas de Cashback.

### H-004 — Transação como fonte de informação

O contexto de Cashback pode consumir informações de transações sem necessariamente assumir a propriedade do domínio de transações.

### H-005 — Integração com parceiros isolada

As particularidades de cada parceiro devem ser isoladas por contratos e mecanismos de integração.

### H-006 — Core Bancário como alternativa

A eventual aquisição de Core Bancário deve ser avaliada em relação às capacidades necessárias e não assumida como solução prévia.

---

# 16. Questões em Aberto

1. O que caracteriza uma transação elegível?
2. Quais produtos podem gerar Cashback?
3. Quem define as regras?
4. Como as regras serão configuradas?
5. Qual é a unidade de cálculo do Cashback?
6. Quando o benefício é considerado concedido?
7. Como são tratados cancelamentos?
8. Como são tratados estornos?
9. Como ocorre a liquidação financeira?
10. Quem financia o Cashback?
11. Como ocorre a reconciliação com os parceiros?
12. Quais informações os parceiros disponibilizam?
13. Como novos parceiros serão incorporados?
14. Quais capacidades existentes podem ser reutilizadas?
15. Quais capacidades poderiam ser fornecidas por um Core Bancário?
16. Quais capacidades devem permanecer no banco?
17. Quais requisitos regulatórios e de segurança se aplicam?
18. Qual arquitetura intermediária será necessária?

---

# 17. Rastreabilidade

A visão estratégica pode ser resumida em:

```text
Driver
  │
  ├── Aumentar portfólio
  │       ↓
  │   Programa de Cashback
  │
  ├── Aumentar engajamento
  │       ↓
  │   Benefícios + Parceiros
  │
  ├── Acelerar lançamentos
  │       ↓
  │   Capacidades reutilizáveis
  │
  └── Reduzir impacto do legado
          ↓
      Desacoplamento
          ↓
      Arquitetura TO-BE
```

---

# 18. Próxima etapa

A evolução recomendada para o cenário é:

```text
Strategy & Motivation
        ↓
Business Architecture
        ↓
Capabilities
        ↓
Value Streams
        ↓
Business Functions
        ↓
Bounded Contexts / Context Map
        ↓
Application Architecture
        ↓
Building Blocks
        ↓
Microservices
        ↓
Technology Architecture
        ↓
Migration Planning
```

A análise do cenário permanece sem conclusão sobre sua priorização frente à Conta de Pagamentos.

O objetivo deste documento é estabelecer a motivação estratégica e a cadeia de rastreabilidade necessária para as próximas fases da arquitetura.
