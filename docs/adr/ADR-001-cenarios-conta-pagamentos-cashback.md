# ADR-001 — Avaliação dos cenários para novo produto bancário

## Status

Em avaliação — decisão não definida.

## Contexto

O banco possui atualmente um portfólio predominantemente baseado em produtos de empréstimos, incluindo Crédito Direto ao Consumidor, Cartão de Crédito, Crédito Pessoal, Consignado e Empréstimos com garantia.

As capacidades desses produtos foram construídas em silos, com pouco reaproveitamento. O legado também impacta a cadeia de valor da companhia.

O C-level identificou dois produtos com resultados positivos nos testes realizados com o público:

1. Conta de Pagamentos.
2. Programa de Cashback com parcerias.

Ambos foram considerados capazes de endereçar o problema de engajamento. A expectativa adicional é que o novo produto contribua para melhorar a arquitetura atual e acelerar o lançamento de novos produtos.

O CTO levantou a possibilidade de aquisição de uma plataforma de Core Bancário como alternativa para endereçar esses problemas. Antes dessa decisão, o CIO solicitou uma análise de Enterprise Architecture.

A análise deve considerar as convenções e boas práticas do setor bancário, mantendo o estilo arquitetural atual baseado em Microservices. Para os elementos que não estiverem aderentes à referência arquitetural vigente, deverá ser considerada uma arquitetura TO-BE e um plano de migração.

## Objetivo do ADR

Registrar os dois cenários de produto identificados no case e suas principais implicações arquiteturais, mantendo a decisão em aberto nesta etapa.

Este ADR não estabelece qual cenário deverá ser adotado.

---

# Cenário 1 — Conta de Pagamentos

## Descrição

O banco habilita uma Conta de Pagamentos como novo produto, utilizando-a como instrumento para ampliar o portfólio e aumentar o engajamento dos clientes.

A solução deve ser analisada considerando sua integração com as capacidades existentes e o impacto do legado atualmente organizado em silos.

## Capacidades e funcionalidades envolvidas

As capacidades e funcionalidades a serem detalhadas durante a evolução da arquitetura incluem:

- Gestão de Conta de Pagamentos.
- Cadastro e manutenção de dados do cliente.
- Abertura e encerramento de conta.
- Movimentação financeira da conta.
- Consulta de saldo e transações.
- Gestão de regras e limites aplicáveis ao produto.
- Integração com capacidades existentes.
- Integração com os componentes legados necessários.
- Exposição e consumo de funcionalidades por meio de serviços.

Esses elementos deverão ser refinados durante o levantamento de capacidades, fluxos de valor e agrupamentos funcionais.

## Implicações arquiteturais

A adoção desse cenário demanda avaliação de:

- Quais capacidades de negócio já existem e podem ser reutilizadas.
- Quais capacidades atualmente estão acopladas aos produtos de crédito.
- Quais capacidades precisam ser desacopladas do legado.
- Quais funcionalidades devem ser implementadas como novos serviços.
- Quais integrações com sistemas existentes serão necessárias.
- Como preservar o estilo arquitetural baseado em Microservices.
- Como evitar que o novo produto replique os silos existentes.
- Como estruturar uma evolução gradual da arquitetura atual para a arquitetura TO-BE.

## Relação com o Core Bancário

A hipótese de aquisição de uma plataforma de Core Bancário deverá ser avaliada neste cenário em relação às capacidades necessárias para suportar a Conta de Pagamentos.

A análise deverá identificar quais capacidades poderiam ser providas pelo Core Bancário, quais permaneceriam sob responsabilidade do banco e quais integrações seriam necessárias.

O case não fornece, nesta etapa, informações suficientes para determinar o conjunto exato de capacidades cobertas por uma eventual plataforma de Core Bancário.

---

# Cenário 2 — Programa de Cashback com Parcerias

## Descrição

O banco habilita um programa de Cashback com parceiros como novo produto, utilizando o programa para ampliar o portfólio e aumentar o engajamento dos clientes.

O cenário deve considerar a capacidade de estabelecer relações com parceiros e administrar as regras de concessão e registro do benefício.

## Capacidades e funcionalidades envolvidas

As capacidades e funcionalidades a serem detalhadas durante a evolução da arquitetura incluem:

- Gestão do programa de Cashback.
- Gestão de parceiros.
- Cadastro e manutenção de parceiros.
- Definição e manutenção das regras de Cashback.
- Elegibilidade de clientes e transações.
- Cálculo do valor de Cashback.
- Registro do Cashback concedido.
- Consulta do histórico de benefícios.
- Integração com produtos e transações existentes.
- Integração com os parceiros.
- Exposição e consumo de funcionalidades por meio de serviços.

Esses elementos deverão ser refinados durante o levantamento de capacidades, fluxos de valor e agrupamentos funcionais.

## Implicações arquiteturais

A adoção desse cenário demanda avaliação de:

- Quais capacidades de negócio podem ser reutilizadas.
- Como representar as regras de Cashback de maneira configurável.
- Como desacoplar a gestão de Cashback dos produtos existentes.
- Como integrar o banco aos parceiros.
- Como garantir interoperabilidade entre as funcionalidades.
- Como registrar e rastrear os benefícios concedidos.
- Como preservar o estilo arquitetural baseado em Microservices.
- Como evitar novos silos funcionais.
- Como evoluir a arquitetura atual para uma arquitetura TO-BE.

## Relação com o Core Bancário

A hipótese de aquisição de uma plataforma de Core Bancário deverá ser avaliada neste cenário em relação às capacidades necessárias para suportar o programa de Cashback.

A análise deverá identificar quais capacidades poderiam ser providas pelo Core Bancário, quais permaneceriam sob responsabilidade do banco e quais integrações seriam necessárias.

O case não fornece, nesta etapa, informações suficientes para determinar o conjunto exato de capacidades cobertas por uma eventual plataforma de Core Bancário.

---

# Elementos comuns aos dois cenários

Independentemente do cenário analisado, o case estabelece alguns direcionadores arquiteturais comuns:

| Direcionador | Aplicação |
|---|---|
| Microservices | O estilo arquitetural existente deve ser preservado. |
| Reuso de capacidades | A solução deve endereçar o problema atual de capacidades construídas em silos. |
| Time-to-Market | A arquitetura deve contribuir para acelerar o lançamento de novos produtos. |
| Interoperabilidade | As funcionalidades devem conseguir interoperar com as capacidades necessárias. |
| Legado | O impacto dos sistemas legados sobre a cadeia de valor deve ser considerado. |
| Arquitetura TO-BE | Elementos não aderentes à referência arquitetural devem ser tratados na arquitetura alvo. |
| Migração | Deve ser considerado um plano de migração da arquitetura atual para a arquitetura alvo. |
| Arquiteturas intermediárias | A transição não precisa ocorrer diretamente do estado atual para o estado final. |
| Building Blocks | Os componentes arquiteturais deverão ser identificados e relacionados às capacidades e funcionalidades. |
| Rastreabilidade | As decisões arquiteturais devem ser vinculadas aos requisitos e problemas de negócio. |

## Questões arquiteturais a serem respondidas

As questões abaixo permanecem abertas para as próximas etapas da análise:

1. Quais capacidades de negócio são necessárias para cada cenário?
2. Quais capacidades já existem no banco?
3. Quais capacidades estão atualmente isoladas em silos?
4. Quais capacidades podem ser reutilizadas?
5. Quais capacidades precisam ser criadas ou transformadas?
6. Quais funcionalidades devem ser agrupadas em cada domínio ou subdomínio?
7. Quais serviços devem ser identificados na arquitetura baseada em Microservices?
8. Quais integrações com o legado serão necessárias?
9. Quais elementos poderiam ser suportados por uma plataforma de Core Bancário?
10. Qual seria o impacto da aquisição de um Core Bancário sobre cada cenário?
11. Quais arquiteturas intermediárias seriam necessárias?
12. Como realizar a migração sem comprometer a cadeia de valor existente?
13. Quais Building Blocks serão necessários para cada cenário?
14. Como cada cenário contribui para o objetivo de acelerar o lançamento de novos produtos?

## Decisão

Não definida neste ADR.

Os dois cenários permanecem em avaliação para as etapas seguintes de Enterprise Architecture, nas quais deverão ser aprofundados o mapa de problemas, capacidades de negócio, fluxos de valor, agrupamentos funcionais, arquitetura TO-BE, arquiteturas intermediárias e estratégia de migração.
