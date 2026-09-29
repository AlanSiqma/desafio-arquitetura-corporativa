# Requisitos Não Funcionais

## Contexto

Requisitos não funcionais e restrições arquiteturais derivados do case de Enterprise Architecture. O objetivo é registrar características esperadas da solução e restrições que deverão orientar a arquitetura.

## Requisitos

| ID | Categoria | Requisito | Origem |
|---|---|---|---|
| RNF-001 | Arquitetura | Manter o estilo arquitetural baseado em Microservices. | Case |
| RNF-002 | Time-to-Market | A arquitetura deve contribuir para acelerar o lançamento de novos produtos. | Case |
| RNF-003 | Reuso | A arquitetura deve aumentar o reaproveitamento de capacidades atualmente construídas em silos. | Case |
| RNF-004 | Interoperabilidade | A solução deve possibilitar a interoperabilidade entre funcionalidades e capacidades necessárias ao negócio. | Derivado do case |
| RNF-005 | Desacoplamento | A evolução dos novos produtos deve reduzir a dependência direta dos sistemas legados em silos. | Derivado do case |
| RNF-006 | Evolução | A arquitetura deve permitir evolução progressiva da arquitetura atual para uma arquitetura TO-BE. | Case |
| RNF-007 | Migração | A solução deve permitir uma estratégia de migração do legado, considerando arquiteturas intermediárias quando necessárias. | Case |
| RNF-008 | Governança | As decisões arquiteturais devem ser justificadas e rastreáveis aos requisitos e problemas de negócio. | Case |
| RNF-009 | Arquitetura Corporativa | A solução deve potencializar os elementos que já estejam aderentes à referência arquitetural vigente. | Case |
| RNF-010 | Arquitetura Corporativa | Os elementos não aderentes devem ser tratados por meio de uma Visão de Arquitetura TO-BE e de um plano de migração. | Case |

## Observações

O requisito RNF-001 é uma restrição explícita do case: a análise deve considerar as boas práticas do setor bancário sem alterar o estilo arquitetural existente, que é Microservices.

Os requisitos relacionados a desacoplamento, interoperabilidade e reuso são derivados dos problemas descritos no case, especialmente da existência de capacidades construídas em silos e do impacto do legado sobre a cadeia de valor.

O material fornecido não especifica métricas quantitativas de disponibilidade, latência, throughput, RTO/RPO, segurança ou volume transacional. Portanto, esses atributos não foram inventados nesta etapa e deverão ser definidos posteriormente caso sejam necessários para a arquitetura.
