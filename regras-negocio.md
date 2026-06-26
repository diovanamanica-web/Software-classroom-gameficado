# Regras de Negócio

## Lista de Regras de Negócio

**RN01 – Criação de Atividades:** Apenas usuários com perfil de "Professor" podem criar, editar ou excluir atividades em uma turma.

**RN02 – Matrícula de Estudantes:** Um estudante só pode acessar os conteúdos e atividades de uma turma se estiver formalmente matriculado nela.

**RN03 – Prazos de Entrega:** O sistema não deve permitir o envio de atividades após a data e horário limite estabelecidos pelo professor, a menos que a opção "aceitar envios com atraso" esteja explicitamente ativada para aquela atividade específica.

**RN04 – Visibilidade de Notas:** As notas de uma avaliação só ficam visíveis para os estudantes após o professor realizar a ação de "Publicar Notas".

**RN05 – Limite de Arquivos:** O tamanho máximo permitido para upload de arquivos em entregas de atividades por estudantes é de 50 MB por arquivo.

**RN06 – Comunicação Oficial:** Toda comunicação no mural da turma deve ser passível de moderação pelo professor responsável, que pode apagar mensagens inadequadas.

**RN07 – Funcionalidade Inovadora (Sala de Aula Gamificada):** Os estudantes recebem pontos de experiência (XP) automaticamente ao entregarem atividades no prazo e ao participarem de fóruns de discussão.

---

## Impacto das Regras de Negócio na Solução

### Impacto da RN01 (Criação de Atividades)
Esta regra influencia profundamente diversos aspectos do sistema:
- **User Story:** Como professor, desejo criar atividades para disponibilizar tarefas aos estudantes.
- **Caso de Uso:** Criar Atividade.
- **BPMN:** No processo de "Publicação de Atividade", a raia (lane) de execução pertence exclusivamente ao Professor.
- **Arquitetura:** Exige a implementação de um mecanismo robusto de controle de acesso baseado em papéis (RBAC - Role-Based Access Control) nos microserviços ou módulos do sistema, garantindo que as rotas de API para criação de atividades verifiquem o token JWT e o perfil do usuário.
- **Requisito Não Funcional:** Segurança e Autorização.

### Impacto da RN03 (Prazos de Entrega)
Esta regra dita o comportamento central do módulo de avaliações:
- **User Story:** Como sistema, desejo bloquear envios de atividades após o prazo estipulado para garantir a isonomia da avaliação.
- **Caso de Uso:** Entregar Atividade.
- **BPMN:** No processo de "Entrega de Atividade", deve haver um gateway exclusivo (XOR) que verifica a condição "Data atual <= Prazo de entrega?". Se falso, o fluxo é direcionado para a rejeição do envio.
- **Arquitetura:** O serviço responsável por receber as submissões deve validar o timestamp da requisição contra o prazo armazenado no banco de dados antes de processar o upload do arquivo no serviço de storage.
- **Decisão Arquitetural:** Uso de sincronização de relógios (NTP) nos servidores para evitar problemas de fuso horário nas entregas.
