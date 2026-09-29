# ADR-002 — Decisão do Cenário para Transformação Arquitetural

## Status

**Aceito**

## Data

2026-09-29

## Decisão

Adotar o **Cashback com Parcerias como primeiro cenário de transformação arquitetural**.

A Conta de Pagamentos permanece como cenário estratégico futuro e não é descartada.

A aquisição de uma plataforma de Core Bancário permanece como uma decisão arquitetural independente e deverá ser submetida posteriormente a uma análise de Capability Fit/Gap.

---

# 1. Contexto

O banco possui um portfólio predominantemente baseado em produtos de crédito.

O case informa que as capacidades desses produtos foram construídas em silos, com pouco reaproveitamento.

Também informa que o legado impacta a cadeia de valor.

O banco deseja:

- aumentar o portfólio;
- aumentar o engajamento;
- acelerar lançamentos de novos produtos;
- melhorar a arquitetura atual.

Foram identificados dois produtos com resultados positivos nos testes com o público:

1. Conta de Pagamentos;
2. Cashback com Parcerias.

O C-level deve priorizar apenas um.

O CTO levantou a possibilidade de aquisição de uma plataforma de Core Bancário.

A arquitetura atual utiliza Microservices e o case determina que esse estilo deve ser preservado.

---

# 2. Problema arquitetural

A decisão não deve considerar somente a habilitação de um novo produto.

O novo produto também deve contribuir para resolver problemas arquiteturais existentes:

```text
Capacidades em silos
        +
Baixo reaproveitamento
        +
Legado impactando a cadeia de valor
        +
Necessidade de acelerar novos lançamentos
```

A pergunta é:

> Qual cenário pode ser utilizado como primeiro veículo de transformação arquitetural sem reproduzir os silos existentes?

---

# 3. Alternativas consideradas

## Alternativa A — Conta de Pagamentos

Criar uma capacidade de Conta de Pagamentos com integração às capacidades existentes e aos componentes legados necessários.

Principais capacidades:

```text
Customer
Product
Account
Transaction
Compliance
Integration
```

## Alternativa B — Cashback com Parcerias

Criar um programa de Cashback com capacidades próprias de benefícios, regras, elegibilidade e parceiros, reutilizando capacidades existentes.

Principais capacidades:

```text
Customer
Product
Transaction
Benefits
Rules
Eligibility
Partner
Compliance
Integration
```

## Alternativa C — Adquirir Core Bancário antes da escolha do produto

Adotar uma plataforma de Core Bancário como solução principal para os problemas arquiteturais.

Esta alternativa foi considerada, mas não possui evidências suficientes no case para ser tomada como decisão neste momento.

---

# 4. Critérios de decisão

A banca avaliou os cenários considerando:

1. contribuição para a transformação arquitetural;
2. potencial de reutilização;
3. dependência do legado;
4. impacto sobre a cadeia de valor;
5. capacidade de criar Building Blocks reutilizáveis;
6. complexidade de integração;
7. possibilidade de evolução incremental;
8. aderência ao estilo Microservices;
9. potencial de acelerar futuros lançamentos;
10. dependência de uma eventual decisão de Core Bancário.

O valor comercial dos produtos não foi utilizado como critério de desempate porque o case informa que ambos apresentaram resultados positivos.

---

# 5. Análise da Conta de Pagamentos

A Conta de Pagamentos introduz uma capacidade bancária estrutural:

```text
Account
```

Ela possui potencial relação com:

```text
Transaction
Balance
Statement
Banking infrastructure
Legacy
Core
```

Isso pode gerar Building Blocks de grande relevância para futuros produtos financeiros.

Entretanto, essa característica também aumenta a profundidade da transformação necessária.

A arquitetura proposta para o cenário contempla:

```text
Customer
Product
Account
Transaction
Integration
Legacy / Core
```

O cenário apresenta maior potencial de transformação da fundação bancária, mas também maior dependência de informações ainda não disponíveis sobre o AS-IS e sobre eventual Core Bancário.

---

# 6. Análise do Cashback

O Cashback introduz capacidades próprias:

```text
Benefits
Rules
Eligibility
Partner
```

Ao mesmo tempo, pode consumir capacidades compartilhadas:

```text
Customer
Product
Transaction
Compliance
Integration
```

O cenário permite uma evolução conceitual:

```text
Transação
    ↓
Elegibilidade
    ↓
Regras
    ↓
Cálculo
    ↓
Benefício
    ↓
Engajamento
```

E:

```text
Partner
    ↓
Integration
    ↓
Benefits
```

Essa separação permite potencialmente construir capacidades reutilizáveis para futuros programas de benefícios.

---

# 7. Trade-offs

## 7.1 Conta de Pagamentos

### Benefícios arquiteturais

- introduz uma capacidade bancária estrutural;
- pode criar Building Blocks reutilizáveis;
- pode contribuir para uma futura fundação de produtos financeiros;
- pode reduzir a dependência de soluções específicas de crédito.

### Custos / riscos arquiteturais

- maior dependência da infraestrutura transacional;
- potencial dependência profunda do legado;
- potencial necessidade de transformação de capacidades financeiras fundamentais;
- maior proximidade com a decisão de Core Bancário;
- necessidade de conhecer melhor o AS-IS para definir a arquitetura intermediária.

---

## 7.2 Cashback

### Benefícios arquiteturais

- cria um domínio de benefícios claramente delimitável;
- permite introduzir novas capacidades de forma incremental;
- pode reutilizar Customer, Product e Transaction;
- pode criar Building Blocks para futuros programas de benefícios;
- permite isolar parceiros;
- pode ser introduzido sem depender imediatamente de uma decisão de Core Bancário.

### Custos / riscos arquiteturais

- integração com parceiros;
- necessidade de contratos de integração;
- necessidade de governança das regras;
- dependência dos dados transacionais;
- risco de criar outro silo caso Benefits seja implementado apenas como funcionalidade do produto;
- necessidade de tratar reversão, conciliação e demais regras operacionais posteriormente.

---

# 8. Razão da decisão

A decisão pelo Cashback não é baseada em uma avaliação de que o produto possui maior valor comercial.

A decisão está baseada no seu papel como **primeiro veículo de transformação arquitetural**.

O Cashback permite introduzir:

```text
Benefits
Rules
Eligibility
Partner
```

como capacidades de negócio explicitamente delimitadas, enquanto potencialmente reutiliza:

```text
Customer
Product
Transaction
```

Isso cria uma oportunidade de demonstrar o princípio arquitetural desejado pelo banco:

```text
Capacidades reutilizáveis
        ↓
Composição
        ↓
Novos produtos
        ↓
Menor duplicação
        ↓
Maior velocidade de evolução
```

---

# 9. Condições da decisão

A decisão está condicionada às seguintes diretrizes.

## 9.1 Não criar novo silo

O Cashback não deve ser implementado como um conjunto isolado de funcionalidades específicas do produto.

## 9.2 Benefits como capacidade própria

A gestão de benefícios deve possuir limite de responsabilidade próprio.

## 9.3 Rules e Eligibility desacoplados

As regras e a elegibilidade devem ser capazes de evoluir sem acoplamento direto aos produtos consumidores.

## 9.4 Partner isolado

Integrações com parceiros devem ser encapsuladas e não devem expor detalhes internos do domínio.

## 9.5 Reuso

Capacidades existentes devem ser reutilizadas quando aderentes.

## 9.6 Isolamento do legado

Dependências do legado devem ser encapsuladas por contratos e mecanismos de integração adequados.

## 9.7 Microservices

A solução deve preservar o estilo arquitetural existente.

---

# 10. Core Bancário

A decisão deste ADR **não aprova nem rejeita a aquisição de Core Bancário**.

A análise futura deverá seguir:

```text
Business Capability
        ↓
Capability necessária
        ↓
Capability oferecida pelo Core
        ↓
Fit / Gap
        ↓
Impacto
        ↓
Migração
        ↓
Custo / benefício
        ↓
Decisão
```

O Core deve ser avaliado como alternativa arquitetural independente.

---

# 11. Consequências positivas

A decisão permite:

- iniciar uma transformação arquitetural incremental;
- criar um novo domínio de benefícios;
- estabelecer novos limites de negócio;
- promover reuso de capacidades existentes;
- criar Building Blocks potencialmente reutilizáveis;
- reduzir o acoplamento direto do novo produto ao legado;
- preservar Microservices;
- criar referência arquitetural para futuros produtos.

---

# 12. Consequências negativas

A decisão também implica:

- novas integrações;
- governança de APIs e eventos;
- gestão de regras;
- integração com parceiros;
- necessidade de isolamento do legado;
- possível coexistência entre arquitetura nova e antiga;
- necessidade de definir arquiteturas intermediárias;
- necessidade de resolver questões operacionais de benefícios.

---

# 13. Riscos

| Risco | Tratamento |
|---|---|
| Cashback virar novo silo | Definir Benefits como capacidade própria |
| Acoplamento ao legado | Isolamento e contratos |
| Regras ficarem espalhadas | Contexto próprio de Rules |
| Integrações com parceiros se tornarem acopladas | Contexto/adapter de Partner |
| Dependência excessiva de Transaction | Contrato explícito |
| Falta de governança | Architecture Governance |
| Arquitetura nova não gerar reuso | Definir Building Blocks reutilizáveis |
| Migração gerar impacto operacional | Arquiteturas intermediárias |

---

# 14. O que permanece em aberto

Este ADR não resolve:

1. decomposição definitiva dos Microservices;
2. definição de APIs;
3. definição de eventos;
4. entidades e agregados táticos;
5. arquitetura tecnológica detalhada;
6. fit/gap de Core Bancário;
7. estratégia detalhada de migração;
8. requisitos quantitativos de disponibilidade, desempenho e volume;
9. detalhes de liquidação e conciliação;
10. regras regulatórias específicas do produto.

Esses pontos serão tratados nas próximas fases.

---

# 15. Próximos passos

A decisão direciona a próxima etapa para:

```text
ADR-002
   ↓
Architecture Vision
   ↓
TO-BE Business Architecture
   ↓
Application Architecture
   ↓
Building Blocks
   ↓
DDD Tático
   ↓
Microservices
   ↓
Arquiteturas Intermediárias
   ↓
Plano de Migração
```

---

# 16. Relação com a Conta de Pagamentos

A Conta de Pagamentos permanece no roadmap arquitetural.

A decisão atual não elimina o cenário.

A hipótese é que as capacidades e padrões arquiteturais estabelecidos com o Cashback possam futuramente servir como referência para novos produtos, inclusive para a Conta de Pagamentos.

Essa relação deverá ser validada durante a evolução da arquitetura.

---

# 17. Rastreabilidade

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
AIP-001 / Conta
 ↓
AIP-002 / Cashback
 ↓
Banca de Arquitetura
 ↓
Trade-offs
 ↓
ADR-002
 ↓
Architecture Vision / TO-BE
```

---

# 18. Decisão final

**Cashback com Parcerias é adotado como primeiro cenário de transformação arquitetural.**

**Conta de Pagamentos permanece como cenário futuro.**

**Core Bancário permanece como alternativa arquitetural a ser avaliada separadamente.**

A decisão deverá ser revisitada caso novas evidências sobre o AS-IS, capacidades existentes, requisitos regulatórios, capacidades de um eventual Core Bancário ou restrições de migração alterem significativamente os trade-offs registrados neste ADR.
