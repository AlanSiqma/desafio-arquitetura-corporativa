# Desafio de Arquitetura Corporativa

Repositório destinado à documentação e evolução da solução para o desafio de Enterprise Architecture.

O objetivo deste trabalho é analisar o cenário apresentado, identificar os problemas de negócio e suas capacidades, avaliar os cenários de produto propostos e construir uma visão arquitetural que permita ao banco evoluir sua arquitetura atual, mantendo o estilo baseado em Microservices.

## Contexto

O banco possui atualmente um portfólio predominantemente baseado em produtos de crédito, como:

* Crédito Direto ao Consumidor;
* Cartão de Crédito;
* Crédito Pessoal;
* Consignado;
* Empréstimos com garantia.

As capacidades existentes foram construídas em silos, com pouco reaproveitamento entre os produtos. Essa característica do legado impacta a cadeia de valor da companhia e dificulta a evolução do portfólio.

Como parte da estratégia de aumento de portfólio e engajamento dos clientes, dois produtos apresentaram resultados positivos nos testes realizados:

* Conta de Pagamentos;
* Programa de Cashback com parcerias.

O desafio consiste em analisar esses cenários sob a perspectiva de Enterprise Architecture, considerando também a hipótese de aquisição de uma plataforma de Core Bancário.

A arquitetura existente utiliza Microservices e esse estilo arquitetural deve ser preservado.

## Objetivos da análise

Este repositório busca documentar, de forma rastreável, a evolução da análise arquitetural:

1. Identificar os problemas de negócio.
2. Identificar e classificar as capacidades de negócio.
3. Levantar e classificar os requisitos.
4. Estabelecer uma linguagem ubíqua.
5. Identificar os subdomínios.
6. Mapear os fluxos de valor.
7. Identificar funcionalidades e agrupamentos funcionais.
8. Avaliar os cenários de Conta de Pagamentos e Cashback.
9. Avaliar os impactos arquiteturais de cada cenário.
10. Identificar Building Blocks.
11. Definir a arquitetura atual (AS-IS).
12. Definir a arquitetura alvo (TO-BE).
13. Identificar arquiteturas intermediárias.
14. Elaborar uma estratégia de migração.
15. Registrar e justificar as decisões arquiteturais.

## Abordagem

A análise será conduzida utilizando conceitos de:

* Enterprise Architecture;
* TOGAF Architecture Development Method (ADM);
* Domain-Driven Design (DDD);
* Domain Storytelling / modelagem de domínio, quando aplicável;
* Arquitetura baseada em Microservices;
* Building Blocks;
* Value Stream / Value Chain;
* Arquitetura AS-IS e TO-BE;
* Architecture Decision Records (ADR).

A intenção é manter rastreabilidade entre negócio e tecnologia:

```text
Problema de Negócio
        ↓
Subdomínio
        ↓
Capacidade de Negócio
        ↓
Fluxo de Valor
        ↓
Requisito
        ↓
Funcionalidade
        ↓
Building Block
        ↓
Microservice / Componente
        ↓
Arquitetura TO-BE
        ↓
Plano de Migração
```

## Cenários em avaliação

### Cenário 1 — Conta de Pagamentos

Avaliação da criação de uma Conta de Pagamentos como novo produto do banco.

O cenário deverá considerar, entre outros aspectos:

* Gestão da conta;
* abertura e encerramento;
* movimentação financeira;
* consulta de saldo e transações;
* integração com capacidades existentes;
* integração com o legado;
* reutilização de capacidades;
* impacto sobre a arquitetura atual;
* potencial utilização de capacidades de uma plataforma de Core Bancário.

### Cenário 2 — Programa de Cashback

Avaliação da criação de um Programa de Cashback com parcerias.

O cenário deverá considerar, entre outros aspectos:

* gestão do programa;
* gestão de parceiros;
* regras de Cashback;
* elegibilidade;
* cálculo do benefício;
* registro do benefício;
* integração com produtos existentes;
* integração com parceiros;
* reutilização de capacidades;
* impacto sobre a arquitetura atual;
* potencial utilização de capacidades de uma plataforma de Core Bancário.

Os dois cenários serão analisados sem pressupor previamente uma decisão arquitetural.

## Repositório

A documentação será organizada progressivamente conforme a evolução da análise.

```text
.
├── README.md
│
└── docs/
    ├── requisitos/
    │   ├── requisitos-funcionais.md
    │   └── requisitos-nao-funcionais.md
    │
    ├── dominio/
    │   └── linguagem-ubiqua.md
    │
    ├── adr/
    │   └── ADR-001-cenarios-conta-pagamentos-cashback.md
    │
    ├── negocio/
    │   ├── problemas-de-negocio.md
    │   ├── subdominios.md
    │   ├── capacidades.md
    │   └── fluxos-de-valor.md
    │
    ├── arquitetura/
    │   ├── as-is/
    │   ├── to-be/
    │   └── building-blocks/
    │
    └── migracao/
        ├── arquiteturas-intermediarias.md
        └── plano-de-migracao.md
```

> A estrutura acima representa a organização pretendida dos artefatos. Novos documentos poderão ser adicionados conforme a análise evoluir.

## Artefatos

### Requisitos

Os requisitos representam as necessidades funcionais, restrições e características arquiteturais identificadas a partir do case.

* [Requisitos Funcionais](docs/requisitos/requisitos-funcionais.md)
* [Requisitos Não Funcionais](docs/requisitos/requisitos-nao-funcionais.md)

### Linguagem Ubíqua

Define o vocabulário comum utilizado entre negócio, arquitetura e tecnologia.

A linguagem ubíqua será utilizada como referência para nomes de domínios, subdomínios, capacidades, funcionalidades e componentes.

* [Linguagem Ubíqua](docs/dominio/linguagem-ubiqua.md)

### Architecture Decision Records

Os ADRs registram decisões, alternativas consideradas, contexto, consequências e questões em aberto.

* [ADR-001 — Cenários Conta de Pagamentos e Cashback](docs/adr/ADR-001-cenarios-conta-pagamentos-cashback.md)

## Princípios arquiteturais

Os seguintes direcionadores são considerados na análise:

### Preservar Microservices

O case estabelece que a análise deve considerar as boas práticas do setor bancário sem alterar o estilo arquitetural existente baseado em Microservices.

### Reduzir silos

A arquitetura deverá buscar maior reutilização das capacidades existentes, evitando reproduzir o cenário atual de capacidades isoladas.

### Evolução incremental

A transformação arquitetural deverá considerar a possibilidade de arquiteturas intermediárias entre o estado atual e o estado alvo.

### Rastreabilidade

As decisões arquiteturais deverão estar relacionadas aos problemas de negócio, requisitos, capacidades e funcionalidades que as justificam.

### Orientação ao negócio

A arquitetura deverá partir das necessidades e capacidades do negócio antes de definir os componentes tecnológicos.

## Critérios de análise

Os cenários serão analisados considerando aspectos como:

| Dimensão       | Questão                                                                        |
| -------------- | ------------------------------------------------------------------------------ |
| Negócio        | Quais problemas e objetivos o cenário endereça?                                |
| Capacidades    | Quais capacidades são necessárias?                                             |
| Reuso          | Quanto das capacidades existentes pode ser reutilizado?                        |
| Integração     | Quais integrações são necessárias?                                             |
| Legado         | Qual impacto existe sobre os sistemas atuais?                                  |
| Arquitetura    | Como o cenário se encaixa na arquitetura baseada em Microservices?             |
| Evolução       | Como a solução pode evoluir ao longo do tempo?                                 |
| Time-to-Market | Como a arquitetura pode contribuir para acelerar novos produtos?               |
| Core Bancário  | Quais capacidades poderiam ser suportadas por uma plataforma de Core Bancário? |
| Migração       | Como sair do AS-IS para o TO-BE?                                               |
| Governança     | Como as decisões serão justificadas e rastreadas?                              |

## Decisões arquiteturais

As decisões não serão tratadas apenas como conclusões isoladas. Cada decisão relevante deverá possuir rastreabilidade para:

```text
Problema
   ↓
Requisito
   ↓
Capacidade
   ↓
Alternativas
   ↓
Trade-offs
   ↓
Decisão
   ↓
Consequências
```

Os ADRs serão utilizados para manter esse histórico.

## Estado atual do trabalho

O trabalho está sendo construído de forma incremental.

### Concluído

* Levantamento inicial de requisitos funcionais.
* Levantamento inicial de requisitos não funcionais.
* Estruturação da linguagem ubíqua.
* Registro inicial dos dois cenários de produto.
* Criação do primeiro ADR.

### Próximas etapas

1. Mapa de problemas de negócio.
2. Identificação dos subdomínios.
3. Mapa de capacidades de negócio.
4. Classificação das capacidades.
5. Value Streams.
6. Value Chain.
7. Mapeamento de funcionalidades.
8. Mapeamento AS-IS.
9. Avaliação arquitetural dos dois cenários.
10. Building Blocks.
11. Arquitetura TO-BE.
12. Arquiteturas intermediárias.
13. Plano de migração.
14. ADRs complementares.
15. Consolidação da recomendação arquitetural.

## Fonte do desafio

O repositório documenta a análise realizada a partir do case de avaliação de Enterprise Architecture.

O case estabelece como pontos de avaliação, entre outros, a identificação de problemas de negócio, conhecimento do TOGAF ADM, classificação de capacidades, mapeamento de requisitos, funcionalidades, padrões de decomposição de Microservices, arquitetura alvo e intermediária, Building Blocks e Value Chain / Value Stream.

## Status

Em desenvolvimento.

A documentação será evoluída conforme novos artefatos e decisões forem produzidos.
