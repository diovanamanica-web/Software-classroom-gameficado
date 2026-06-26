# Diário de Sprint

## Divisão das Responsabilidades
Para a elaboração deste projeto, as responsabilidades foram divididas simulando o trabalho de uma equipe ágil multidisciplinar:
- **Product Owner (PO):** Responsável por definir a Visão do Produto, mapear os Stakeholders, elicitar as Regras de Negócio e escrever as User Stories, garantindo que o MVP atendesse às necessidades do cliente.
- **Arquiteto de Software:** Responsável por definir a arquitetura de microserviços, modelar os diagramas C4 (Contexto e Containers) e documentar as decisões arquiteturais, garantindo a viabilidade técnica, escalabilidade e segurança da solução.
- **Analista de Processos / Engenheiro de Requisitos:** Responsável por modelar o processo de negócio em BPMN e criar o diagrama de Casos de Uso em UML.
- **Scrum Master / Agile Coach:** Responsável por organizar o repositório GitHub, configurar o quadro Kanban (Gestor de Projetos) e redigir este Diário de Sprint.

## Principais Decisões Tomadas
1. **Foco do MVP:** Decidimos restringir o MVP estritamente ao fluxo de "Criar Turma -> Publicar Atividade -> Entregar Atividade -> Atribuir Nota". Qualquer funcionalidade fora desse fluxo crítico foi movida para o backlog futuro.
2. **Arquitetura de Microserviços:** Optamos por microserviços em vez de monolito devido à necessidade de escalabilidade independente, especialmente para o serviço de entrega de atividades que sofre picos de uso.
3. **Funcionalidade Inovadora:** Escolhemos a Gamificação (atribuição de XP por entregas no prazo) como diferencial competitivo, pois ataca diretamente o problema de engajamento dos alunos em ambientes virtuais.

## Dificuldades Encontradas
- **Modelagem do BPMN:** Houve um desafio inicial em representar corretamente a verificação do prazo de entrega de forma clara sem poluir o diagrama.
- **Isolamento da Gamificação:** Integrar a funcionalidade inovadora sem aumentar o acoplamento do sistema principal exigiu uma reflexão cuidadosa sobre a arquitetura.

## Soluções Adotadas
- **BPMN:** Utilizamos um gateway exclusivo (XOR) simples no diagrama para representar a verificação de prazo (RN03), mantendo o fluxo legível e direto.
- **Arquitetura Orientada a Eventos:** Para resolver o acoplamento da gamificação, adotamos uma estratégia de mensageria assíncrona (Publish-Subscribe). O serviço de atividades apenas emite um evento de sucesso, e o serviço de gamificação o consome quando possível, sem bloquear a experiência do usuário.
