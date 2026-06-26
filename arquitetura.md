# Arquitetura de Software

## Estilo Arquitetural Escolhido: Microserviços
Para o Sistema de Gestão de Sala de Aula Online, optamos pela arquitetura baseada em **Microserviços**. Esta decisão foi tomada visando alta escalabilidade, isolamento de falhas e flexibilidade tecnológica.

### Justificativa da Escolha
Em um ambiente educacional, o uso do sistema sofre picos extremos de acesso em horários específicos (ex: véspera de provas, prazos finais de entrega de trabalhos). A arquitetura de microserviços permite que escalemos apenas as partes do sistema que estão sob alta demanda (como o serviço de entrega de atividades) sem precisar escalar todo o monolito. Além disso, a funcionalidade inovadora de gamificação pode ser desenvolvida, implantada e mantida de forma totalmente independente do núcleo do sistema.

## Decisões Arquiteturais Relevantes

### 1. Mecanismo de Autenticação (JWT via API Gateway)
- **Decisão:** Utilização de JSON Web Tokens (JWT) gerados por um serviço de autenticação dedicado e validados no API Gateway.
- **Justificativa:** Como a arquitetura é distribuída, a autenticação baseada em sessão (stateful) exigiria sincronização complexa entre os serviços. O JWT permite uma abordagem stateless, onde o API Gateway valida o token e repassa as informações do usuário (ID, Role) nos headers para os microserviços internos. Isso atende perfeitamente à Regra de Negócio RN01 (Controle de acesso para criação de atividades).

### 2. Estratégia de Armazenamento de Arquivos (Cloud Storage - S3)
- **Decisão:** Todos os arquivos (materiais didáticos e entregas de alunos) serão armazenados diretamente em um serviço de Cloud Storage (como AWS S3), com o banco de dados armazenando apenas as URLs e metadados.
- **Justificativa:** Arquivos multimídia e documentos pesam rapidamente no armazenamento e na banda de rede. Transferir a responsabilidade do armazenamento e entrega (download) desses arquivos para um serviço especializado em nuvem (S3) alivia a carga sobre os microserviços e garante alta disponibilidade, além de facilitar a imposição da regra de limite de 50MB (RN05).

### 3. Comunicação Assíncrona para Gamificação (Publish-Subscribe)
- **Decisão:** Utilização de um Message Broker (ex: RabbitMQ ou Kafka) para comunicação entre o Serviço de Atividades e o Serviço de Gamificação.
- **Justificativa:** Quando um aluno entrega uma atividade no prazo, o sistema precisa calcular e atribuir XP (RN07). Para evitar que uma falha no serviço de gamificação impeça o aluno de entregar a atividade (que é a funcionalidade crítica), o Serviço de Atividades apenas publica um evento "AtividadeEntregue". O Serviço de Gamificação consome esse evento assincronamente. Isso garante baixo acoplamento e alta resiliência.

## Diagramas C4
Os diagramas arquiteturais estão disponíveis na pasta `/c4` do repositório:
- `c4/contexto.png` (Nível 1)
- `c4/containers.png` (Nível 2)
