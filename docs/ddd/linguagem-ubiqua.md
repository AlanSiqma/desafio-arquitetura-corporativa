# Linguagem Ubíqua — Case Enterprise Architecture

## Objetivo

Estabelecer um vocabulário comum entre negócio, Enterprise Architecture, tecnologia e demais participantes do domínio, reduzindo ambiguidades entre os conceitos utilizados no case.

A linguagem abaixo é derivada dos termos e problemas apresentados no case. Termos que não são explicitamente definidos no material são marcados como **interpretação para alinhamento** e deverão ser validados com os stakeholders.

## Glossário

| Termo | Definição no contexto do case | Tipo | Termos relacionados |
|---|---|---|---|
| Banco | Instituição financeira do case, localizada em São Paulo e responsável pelo portfólio de produtos analisado. | Domínio | Cliente, Produto |
| Cliente | Pessoa que utiliza os produtos e serviços disponibilizados pelo banco. | Domínio | Produto, Engajamento |
| Produto | Oferta financeira ou de relacionamento disponibilizada pelo banco ao cliente. | Domínio | Conta de Pagamentos, Cashback |
| Conta de Pagamentos | Produto candidato destinado a ampliar o portfólio e contribuir para o engajamento dos clientes. | Produto | Cliente, Movimentação |
| Cashback | Benefício associado ao programa de parcerias, no qual o cliente recebe um retorno conforme regras estabelecidas. | Produto | Parceiro, Regra de Cashback |
| Programa de Cashback | Produto ou conjunto de funcionalidades destinado à concessão e gestão de Cashback em parceria com outras empresas. | Produto | Cashback, Parceiro |
| Parceiro | Organização participante do Programa de Cashback. | Domínio | Programa de Cashback, Regra de Cashback |
| Regra de Cashback | Critério que determina a elegibilidade e/ou o valor do Cashback. | Negócio | Cashback, Parceiro |
| Engajamento | Resultado de negócio esperado com a ampliação do portfólio de produtos. | Negócio | Cliente, Produto |
| Portfólio de Produtos | Conjunto de produtos disponibilizados pelo banco. | Negócio | Produto, Empréstimos |
| Capacidade de Negócio | Habilidade que a organização precisa possuir para executar uma determinada atividade de negócio, independentemente de sua implementação tecnológica. | Arquitetura | Subdomínio, Funcionalidade |
| Subdomínio | Recorte do domínio de negócio utilizado para organizar problemas e responsabilidades relacionados. | Arquitetura/DDD | Domínio, Capacidade |
| Funcionalidade | Comportamento ou ação que uma solução deve disponibilizar para suportar uma capacidade ou requisito. | Solução | Capacidade, Microservice |
| Fluxo de Valor | Sequência de atividades que entrega valor ao cliente ou a outro interessado. | Negócio/Arquitetura | Capacidade, Produto |
| Cadeia de Valor | Organização dos fluxos e atividades que contribuem para a geração de valor da companhia. | Negócio/Arquitetura | Fluxo de Valor |
| Legado | Sistemas e componentes existentes que suportam o portfólio atual e influenciam a evolução da arquitetura. | Tecnologia | Silos, Migração |
| Silo | Estrutura na qual capacidades ou funcionalidades foram construídas de forma isolada, com pouco reaproveitamento. | Arquitetura | Legado, Reuso |
| Reuso de Capacidade | Utilização de uma capacidade existente por mais de um produto ou fluxo de negócio. | Arquitetura | Capacidade, Produto |
| Interoperabilidade | Capacidade de diferentes funcionalidades, serviços ou sistemas trabalharem conjuntamente por meio de integrações definidas. | Arquitetura | Integração, Microservices |
| Microservice | Unidade de serviço da arquitetura baseada em Microservices, associada a uma responsabilidade delimitada. | Tecnologia | Capacidade, Funcionalidade |
| Serviço | Componente tecnológico que disponibiliza uma ou mais funcionalidades por meio de uma interface definida. | Tecnologia | Microservice, API |
| API | Interface utilizada para comunicação entre serviços, aplicações ou capacidades expostas tecnologicamente. | Tecnologia | Serviço, Integração |
| Integração | Mecanismo pelo qual sistemas, serviços ou componentes trocam informações ou acionam funcionalidades uns dos outros. | Tecnologia | API, Interoperabilidade |
| Core Bancário | Plataforma considerada pelo CTO como possível aquisição para suportar capacidades bancárias e endereçar parte dos problemas atuais. | Tecnologia/Negócio | Capacidade, Legado |
| Arquitetura Atual (AS-IS) | Representação do estado atual da arquitetura, incluindo os produtos, capacidades e sistemas existentes. | Arquitetura | Legado, Silo |
| Arquitetura Alvo (TO-BE) | Estado arquitetural futuro proposto para endereçar os problemas identificados e orientar a evolução da arquitetura. | Arquitetura | Migração, Building Block |
| Arquitetura Intermediária | Estado arquitetural utilizado durante a transição entre a arquitetura atual e a arquitetura alvo. | Arquitetura | Migração, TO-BE |
| Migração | Processo de evolução da arquitetura atual para a arquitetura alvo. | Arquitetura | Legado, TO-BE |
| Building Block | Bloco reutilizável da arquitetura utilizado para representar uma capacidade, componente ou elemento arquitetural. | Arquitetura | Capacidade, Microservice |
| Requisito Funcional | Comportamento ou funcionalidade que a solução deve oferecer. | Requisito | Funcionalidade |
| Requisito Não Funcional | Restrição ou característica de qualidade que deve orientar a solução. | Requisito | Arquitetura |
| Referência Arquitetural | Conjunto de convenções e boas práticas utilizadas como referência para avaliar a aderência da arquitetura. | Arquitetura | TO-BE, Governança |
| Aderência Arquitetural | Grau em que um elemento da arquitetura atual está alinhado à referência arquitetural vigente. | Arquitetura | Referência Arquitetural |
| Enterprise Architecture | Disciplina responsável, neste case, por analisar problemas de negócio, capacidades, arquitetura atual e futura e orientar a evolução arquitetural. | Governança | TOGAF, Arquitetura |
| TOGAF ADM | Método de desenvolvimento de arquitetura utilizado como referência para conduzir a análise e evolução arquitetural. | Framework | Enterprise Architecture |
| DDD | Abordagem utilizada para alinhar a estrutura da solução aos conceitos e limites do domínio de negócio. | Abordagem | Subdomínio, Linguagem Ubíqua |
| Linguagem Ubíqua | Vocabulário compartilhado entre especialistas de negócio e tecnologia para representar conceitos do domínio de forma consistente. | DDD | Domínio, Subdomínio |
| Domínio | Espaço de conhecimento e atividade de negócio que está sendo modelado. | DDD | Subdomínio, Capacidade |

## Termos que precisam de validação com o negócio

Alguns conceitos podem ser refinados após entrevistas ou workshops com os stakeholders:

- O significado operacional de **Conta de Pagamentos** dentro do banco.
- As operações financeiras que a Conta de Pagamentos deverá suportar.
- A definição de **Cashback** e as condições para sua concessão.
- O conceito de **Parceiro** e o modelo de relacionamento com o banco.
- As regras de elegibilidade do cliente.
- A forma de cálculo e liquidação do Cashback.
- Quais capacidades devem ser consideradas parte do **Core Bancário**.
- Quais capacidades devem permanecer sob responsabilidade do banco.
- O significado quantitativo de **acelerar o lançamento de novos produtos**.
- Quais critérios serão utilizados para determinar **aderência arquitetural**.

## Regras para utilização da linguagem

1. Um mesmo conceito deve utilizar o mesmo termo em documentos, diagramas, requisitos, APIs e discussões de arquitetura.
2. Termos técnicos não devem substituir conceitos de negócio quando o conceito de negócio já estiver estabelecido.
3. Novos termos devem ser incorporados ao glossário quando surgirem durante workshops de domínio.
4. Se um termo possuir significados diferentes entre áreas, o conflito deve ser explicitado e resolvido antes de utilizá-lo como conceito arquitetural.
5. Os nomes de capacidades, subdomínios, funcionalidades e serviços devem permanecer rastreáveis aos termos definidos na linguagem ubíqua.

## Relação com os próximos artefatos

A linguagem ubíqua deverá servir como base para:

`Linguagem Ubíqua → Subdomínios → Capacidades → Fluxos de Valor → Funcionalidades → Building Blocks → Microservices`

Essa relação permite manter o vocabulário de negócio conectado aos artefatos de arquitetura e à futura decomposição da solução.
