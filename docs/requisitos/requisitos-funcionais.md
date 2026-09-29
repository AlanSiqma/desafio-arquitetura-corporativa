# Requisitos Funcionais

## Contexto

Requisitos funcionais derivados do case de Enterprise Architecture, considerando o problema de negócio apresentado e os produtos candidatos: Conta de Pagamentos e Programa de Cashback com parcerias.

## Requisitos

| ID | Categoria | Requisito | Origem |
|---|---|---|---|
| RF-001 | Produto | Permitir a disponibilização de uma Conta de Pagamentos. | Case |
| RF-002 | Produto | Permitir a utilização da Conta de Pagamentos nas operações previstas pelo novo produto. | Derivado do case |
| RF-003 | Produto | Permitir a disponibilização de um programa de Cashback com parceiros. | Case |
| RF-004 | Cashback | Permitir o cadastro e a gestão de parceiros do programa de Cashback. | Derivado do case |
| RF-005 | Cashback | Permitir a definição e manutenção das regras de Cashback. | Derivado do case |
| RF-006 | Cashback | Permitir o cálculo do valor de Cashback conforme as regras estabelecidas. | Derivado do case |
| RF-007 | Cashback | Permitir o registro do Cashback concedido ao cliente. | Derivado do case |
| RF-008 | Integração | Permitir a integração do novo produto com as capacidades e sistemas existentes do banco. | Derivado do case |
| RF-009 | Integração | Permitir a interoperabilidade entre as funcionalidades necessárias ao novo produto. | Derivado do case |
| RF-010 | Produtos | Permitir a reutilização de capacidades existentes na composição de novos produtos. | Derivado do problema de silos |

## Observações

Os requisitos RF-001 e RF-003 representam diretamente os dois produtos apresentados no case. Os demais são requisitos funcionais derivados dos problemas e objetivos descritos no material.

O case informa que o portfólio atual é predominantemente formado por produtos de empréstimos e que suas capacidades foram construídas em silos, com pouco reaproveitamento. Também estabelece a necessidade de considerar oportunidades de melhoria das operações com base nas capacidades de negócio identificadas.
