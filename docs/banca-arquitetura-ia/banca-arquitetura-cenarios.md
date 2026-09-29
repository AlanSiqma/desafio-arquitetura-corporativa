# Banca de Arquitetura — Avaliação dos Cenários de Produto

## 1. Objetivo

Este documento registra a discussão simulada de uma **Banca de Arquitetura Corporativa** para avaliar os dois cenários apresentados no case:

1. Conta de Pagamentos.
2. Cashback com Parcerias.

A banca utiliza como base os artefatos já produzidos para o desafio:

- Strategy & Motivation;
- requisitos funcionais e não funcionais;
- problemas e subdomínios;
- capacidades de negócio;
- arquitetura AS-IS;
- Bounded Contexts;
- Context Map;
- Business Architecture;
- AIPs dos dois cenários;
- ADR-001.

O objetivo da banca não é avaliar qual produto possui maior valor comercial. O case já informa que os dois produtos apresentaram resultados positivos nos testes com o público.

O objetivo é avaliar **qual cenário oferece melhores condições para funcionar como primeiro veículo de evolução arquitetural**, considerando o problema estrutural apresentado pelo banco.

---

# 2. Contexto da decisão

O case apresenta um banco cujo portfólio atual é predominantemente baseado em produtos de crédito.

As capacidades existentes foram construídas em silos e apresentam pouco reaproveitamento.

O legado também impacta a cadeia de valor.

Ao mesmo tempo, o banco deseja:

- ampliar o portfólio;
- aumentar o engajamento;
- acelerar o lançamento de novos produtos;
- melhorar a arquitetura atual;
- preservar o estilo arquitetural baseado em Microservices.

O case apresenta dois produtos candidatos:

```text
Conta de Pagamentos
        ou
Cashback com Parcerias
```

Também existe uma hipótese levantada pelo CTO:

```text
Aquisição de uma plataforma de Core Bancário
```

A banca deve avaliar essa hipótese sem tratá-la como premissa.

---

# 3. Pergunta arquitetural

A pergunta central da banca é:

> Qual dos dois cenários oferece melhores condições para habilitar um novo produto e, simultaneamente, servir como primeiro caso de transformação da arquitetura atual, aumentando reutilização, reduzindo dependências de silos e contribuindo para acelerar futuros lançamentos?

---

# 4. Perspectivas da banca

Foram consideradas quatro perspectivas arquiteturais complementares.

## 4.1 Enterprise Architecture / Estratégia

### Preocupação

Garantir que a escolha do produto também contribua para os objetivos arquiteturais estratégicos.

### Observação

O problema não é apenas criar mais um produto.

Existe uma combinação de objetivos:

```text
Aumentar portfólio
        +
Aumentar engajamento
        +
Acelerar novos lançamentos
        +
Melhorar arquitetura
```

A escolha deve, portanto, considerar o efeito do novo produto sobre a capacidade futura do banco.

### Parecer

A escolha deve privilegiar uma solução que possa introduzir novas capacidades sem reproduzir o padrão atual de silos.

O Cashback apresenta uma oportunidade de introduzir uma nova capacidade transversal de benefícios, potencialmente reutilizável por outros produtos.

---

# 5. Perspectiva DDD / Business Architecture

## 5.1 Conta de Pagamentos

O cenário possui um domínio central claramente identificável:

```text
Customer
   ↓
Account
   ↓
Transaction
   ↓
Balance / Statement
```

A Conta de Pagamentos representa uma capacidade bancária estrutural.

Entretanto, sua implementação possui potencial dependência de capacidades financeiras fundamentais e do legado.

## 5.2 Cashback

O cenário apresenta um conjunto de conceitos próprios:

```text
Programa
Benefício
Regra
Elegibilidade
Parceiro
Cashback
Concessão
```

A modelagem permite identificar um possível domínio de benefícios separado dos produtos existentes.

Também permite reutilizar potencialmente:

```text
Customer
Product
Transaction
Compliance
Integration
```

e adicionar:

```text
Benefits
Rules
Eligibility
Partner
```

### Parecer

O Cashback apresenta limites de domínio que podem ser introduzidos de forma incremental, sem necessariamente exigir a reconstrução imediata da fundação transacional do banco.

---

# 6. Perspectiva Banking / Core

A Conta de Pagamentos possui maior proximidade com capacidades bancárias fundamentais.

Uma eventual plataforma de Core Bancário poderia potencialmente fornecer capacidades relacionadas a:

```text
Account
Transaction
Ledger
Balance
Settlement
```

Entretanto, o case não informa quais capacidades uma eventual plataforma forneceria.

Também não existem dados suficientes neste estágio sobre:

- cobertura funcional;
- aderência;
- custos;
- migração;
- impactos operacionais;
- integrações;
- impacto regulatório;
- dependências.

Portanto, a banca não considera válida a seguinte conclusão:

```text
Conta de Pagamentos
        ↓
Necessidade de Core Bancário
```

O Core deve ser avaliado separadamente por meio de um Capability Fit/Gap.

### Parecer

A aquisição de Core Bancário não deve ser uma pré-condição para a decisão do produto.

---

# 7. Perspectiva Arquitetura / Migração

A decisão precisa ser compatível com uma evolução incremental.

## Conta de Pagamentos

Hipótese de evolução:

```text
AS-IS
Silos / Legado
      ↓
Account
      ↓
Transaction
      ↓
Legacy / Core
      ↓
TO-BE
```

Essa evolução pode envolver uma transformação mais profunda da fundação bancária.

## Cashback

Hipótese de evolução:

```text
AS-IS
Produtos existentes
      ↓
Transaction
      ↓
Benefits
      ↓
Rules
      ↓
Eligibility
      ↓
Partner
```

Existe a possibilidade de introduzir o novo domínio progressivamente e isolá-lo do legado por meio de contratos e mecanismos de integração.

### Parecer

O Cashback apresenta uma oportunidade de transformação incremental mais diretamente compatível com a situação descrita no case.

---

# 8. Trade-offs

## 8.1 Valor de negócio

Os dois produtos apresentaram resultados positivos nos testes realizados com o público.

Portanto, os artefatos arquiteturais não possuem evidência suficiente para diferenciar os produtos por valor comercial.

**Resultado:** critério não utilizado como desempate arquitetural.

---

## 8.2 Transformação arquitetural

### Conta de Pagamentos

Introduz uma capacidade financeira fundamental:

```text
Account
```

e potencialmente impacta:

```text
Transaction
Balance
Statement
Banking infrastructure
```

### Cashback

Introduz principalmente:

```text
Benefits
Rules
Eligibility
Partner
```

sobre capacidades existentes.

**Trade-off:** Conta possui potencial de transformação estrutural maior; Cashback possui potencial de transformação incremental maior.

---

## 8.3 Reutilização

### Conta

Potencialmente reutiliza:

```text
Customer
Product
Transaction
Compliance
Integration
```

mas precisa introduzir uma capacidade central de conta.

### Cashback

Potencialmente reutiliza:

```text
Customer
Product
Transaction
Compliance
Integration
```

e adiciona:

```text
Benefits
Rules
Eligibility
Partner
```

**Trade-off:** Cashback apresenta maior potencial de demonstrar composição de capacidades existentes.

---

## 8.4 Dependência do legado

### Conta

Possível cadeia:

```text
Account
   ↓
Transaction
   ↓
Legacy / Core
```

### Cashback

Possível cadeia:

```text
Transaction
   ↓
Benefits
```

com integração com parceiros.

**Trade-off:** Conta possui potencial de dependência mais profunda da fundação bancária; Cashback possui dependências externas e de integração com parceiros.

---

## 8.5 Complexidade de integração

### Conta

Principalmente:

```text
Canais
Account
Transaction
Banking infrastructure
Legacy / Core
```

### Cashback

Principalmente:

```text
Transaction
Benefits
Rules
Partner
External integrations
```

**Trade-off:** as complexidades são diferentes e não existe informação suficiente para afirmar que uma é quantitativamente menor.

---

## 8.6 Core Bancário

A Conta possui maior relação conceitual com uma plataforma de Core Bancário.

Isso não significa que o Core seja necessário.

O Cashback possui menor dependência conceitual dessa decisão.

**Trade-off:** escolher Conta pode tornar a discussão de Core mais imediata; escolher Cashback permite postergar essa decisão enquanto a avaliação de capabilities é realizada.

---

## 8.7 Capacidade de servir como referência para futuros produtos

O objetivo arquitetural é acelerar futuros lançamentos.

O Cashback pode estabelecer Building Blocks e capacidades reutilizáveis relacionados a:

```text
Benefits
Rules
Eligibility
Partner
```

que podem potencialmente ser utilizados em outros programas de relacionamento e benefícios.

A Conta pode estabelecer Building Blocks relacionados a:

```text
Account
Transaction
Balance
Statement
```

que possuem alto potencial de reutilização em produtos financeiros.

**Trade-off:** ambos possuem potencial de gerar Building Blocks; eles atuam em diferentes partes da arquitetura bancária.

---

# 9. Pergunta crítica da banca

A banca deve evitar que o Cashback simplesmente se torne outro silo.

Uma arquitetura inadequada seria:

```text
Legacy Product A ──┐
Legacy Product B ──┼── Cashback
Legacy Product C ──┘
```

Isso apenas adicionaria mais um produto.

A direção arquitetural pretendida é:

```text
                 Customer
                    │
                 Product
                    │
                Transaction
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
 Existing Products        Benefits
                              │
                     ┌────────┼────────┐
                     ↓        ↓        ↓
                   Rules  Eligibility Partner
```

O Cashback só representa uma melhoria arquitetural se suas capacidades forem modeladas como componentes de negócio reutilizáveis e não como um silo específico do produto.

---

# 10. Condições arquiteturais para o Cashback

Caso o cenário seja adotado como primeiro veículo de transformação, a banca estabelece as seguintes condições:

### Condição 1 — Benefits como domínio próprio

A gestão de benefícios não deve ser espalhada pelos produtos consumidores.

### Condição 2 — Regras desacopladas

As regras do programa devem possuir responsabilidade própria, permitindo evolução independente.

### Condição 3 — Elegibilidade explícita

A avaliação de elegibilidade deve possuir responsabilidade claramente delimitada.

### Condição 4 — Parceiros isolados

Integrações com parceiros devem ser isoladas do núcleo de benefícios.

### Condição 5 — Reuso de capacidades

Customer, Product, Transaction e demais capacidades existentes devem ser reutilizadas quando adequadas.

### Condição 6 — Isolamento do legado

O novo domínio não deve depender diretamente de detalhes internos dos sistemas legados.

### Condição 7 — Microservices preservado

A evolução deve manter o estilo arquitetural definido pelo case.

---

# 11. Posição sobre Core Bancário

A banca recomenda que Core Bancário seja tratado como uma decisão arquitetural independente.

A próxima análise deve ser:

```text
Business Capabilities
        ↓
Capabilities necessárias
        ↓
Capabilities oferecidas pelo Core
        ↓
Fit / Gap
        ↓
Impactos
        ↓
Migração
        ↓
Decisão de Core
```

Não é recomendável tomar a decisão de Core apenas com base na escolha do produto.

---

# 12. Parecer consolidado

A banca consolida o seguinte parecer:

> O Cashback com Parcerias deve ser utilizado como primeiro cenário de transformação arquitetural, mantendo a Conta de Pagamentos como cenário estratégico posterior e não descartado.

A justificativa arquitetural é:

> Dado que o problema central do case envolve capacidades construídas em silos, baixo reaproveitamento, impacto do legado na cadeia de valor e necessidade de acelerar novos lançamentos, o Cashback oferece uma oportunidade de introduzir novas capacidades de benefícios, regras, elegibilidade e parceiros de forma incremental, reutilizando capacidades existentes e preservando o estilo Microservices.

A decisão não significa que Cashback seja superior como produto comercial.

A decisão significa que ele apresenta, com as evidências disponíveis, uma oportunidade mais adequada para funcionar como **primeiro veículo de transformação arquitetural**.

---

# 13. O que a decisão não estabelece

Esta banca não estabelece que:

- Conta de Pagamentos deve ser descartada;
- Core Bancário deve ser rejeitado;
- Cashback possui menor risco absoluto;
- Cashback possui maior retorno financeiro;
- todos os sistemas necessários já existem;
- todas as capacidades identificadas estão disponíveis no AS-IS.

Esses pontos exigem análises específicas.

---

# 14. Próxima evolução arquitetural

Após a decisão:

```text
Banca
  ↓
ADR-002 — Decisão
  ↓
Architecture Vision
  ↓
TO-BE
  ↓
Building Blocks
  ↓
Application Architecture
  ↓
Microservices
  ↓
Arquiteturas Intermediárias
  ↓
Plano de Migração
```

---

# 15. Rastreabilidade

```text
Case
 ↓
Problemas de negócio
 ↓
Strategy & Motivation
 ↓
Value Streams
 ↓
Business Architecture
 ↓
Capabilities
 ↓
Bounded Contexts
 ↓
Context Map
 ↓
Trade-offs
 ↓
Banca de Arquitetura
 ↓
ADR-002
```
