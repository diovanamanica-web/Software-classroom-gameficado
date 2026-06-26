# User Stories

**US01 - Criação de Turma**
- **Descrição:** Como professor, desejo criar uma nova turma virtual para organizar meus alunos e materiais didáticos.
- **Critérios de Aceitação:**
  - O professor deve poder informar o nome da disciplina, código e descrição.
  - O sistema deve gerar um código único de convite para a turma.
  - A turma recém-criada deve aparecer imediatamente no painel do professor.

**US02 - Matrícula via Código**
- **Descrição:** Como estudante, desejo ingressar em uma turma utilizando um código de convite para ter acesso aos conteúdos da disciplina.
- **Critérios de Aceitação:**
  - O estudante deve ter um campo para inserir o código alfanumérico.
  - O sistema deve validar se o código existe e está ativo.
  - Após validação, o estudante deve ser adicionado à lista de membros da turma.

**US03 - Publicação de Material Didático**
- **Descrição:** Como professor, desejo publicar arquivos (PDFs, apresentações) e links no mural da turma para disponibilizar conteúdo de estudo.
- **Critérios de Aceitação:**
  - O professor deve poder fazer upload de arquivos de até 50 MB.
  - O professor deve poder adicionar uma descrição ao material.
  - Todos os alunos da turma devem ser notificados da nova publicação.

**US04 - Criação de Atividade com Prazo**
- **Descrição:** Como professor, desejo criar uma atividade com data e hora limite de entrega para avaliar o conhecimento dos alunos.
- **Critérios de Aceitação:**
  - O formulário deve conter título, instruções, pontuação máxima e data/hora limite.
  - A atividade deve aparecer no calendário/agenda da turma.

**US05 - Entrega de Atividade**
- **Descrição:** Como estudante, desejo fazer o upload de um arquivo como resposta a uma atividade proposta para ser avaliado pelo professor.
- **Critérios de Aceitação:**
  - O sistema deve permitir o upload de arquivos.
  - O sistema deve registrar a data e hora exatas do envio.
  - O sistema deve bloquear o envio se o prazo estiver expirado (conforme RN03).

**US06 - Correção e Feedback**
- **Descrição:** Como professor, desejo atribuir uma nota e um comentário a uma atividade entregue por um estudante para fornecer feedback sobre seu desempenho.
- **Critérios de Aceitação:**
  - O professor deve poder visualizar o arquivo enviado pelo aluno.
  - Deve haver um campo numérico para a nota (respeitando a pontuação máxima).
  - Deve haver um campo de texto para comentários.
  - O aluno deve ser notificado quando a nota for publicada.

**US07 - Visualização de Notas**
- **Descrição:** Como estudante, desejo visualizar minhas notas e feedbacks em um painel centralizado para acompanhar meu desempenho acadêmico.
- **Critérios de Aceitação:**
  - O painel deve listar todas as atividades avaliadas da turma.
  - Deve exibir a nota obtida versus a nota máxima.
  - Deve exibir os comentários do professor.

**US08 - Funcionalidade Inovadora: Sistema de Recompensas (Gamificação)**
- **Descrição:** Como estudante, desejo receber pontos de experiência (XP) ao entregar atividades no prazo para me sentir motivado a manter minhas tarefas em dia.
- **Critérios de Aceitação:**
  - O sistema deve creditar uma quantidade fixa de XP automaticamente após um envio bem-sucedido dentro do prazo.
  - O perfil do aluno deve exibir seu nível e total de XP atual.
  - Deve haver um ranking (leaderboard) opcional visível para a turma.
