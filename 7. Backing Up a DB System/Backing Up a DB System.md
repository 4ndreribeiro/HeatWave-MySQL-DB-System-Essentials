Backup de um DB System MySQL HeatWave
O backup de seu DB System MySQL HeatWave na Oracle Cloud Infrastructure (OCI) é uma funcionalidade crucial para a recuperação de desastres, proteção de dados contra perdas acidentais e conformidade. O serviço MySQL HeatWave oferece mecanismos de backup flexíveis, incluindo backups automáticos e manuais, bem como opções de restauração.

1. Visão Geral dos Backups no MySQL HeatWave
O serviço MySQL HeatWave no OCI simplifica o processo de backup ao gerenciar a maioria das operações para você. Os backups são armazenados no Oracle Cloud Infrastructure Object Storage, garantindo durabilidade e alta disponibilidade.

Existem dois tipos principais de backups:

Backups Automáticos: Programados e gerenciados pelo serviço, com base nas configurações que você define.

Backups Manuais (Sob Demanda): Iniciados por você a qualquer momento, úteis para pontos de recuperação específicos antes de grandes mudanças.

2. Backups Automáticos
Os backups automáticos são a primeira linha de defesa contra perda de dados. Eles são habilitados por padrão e configuráveis durante a criação do DB System ou posteriormente.

2.1. Configurando Backups Automáticos
Durante a criação do DB System:

Na seção "Configurar backup", você pode definir a Janela de backup e o Período de retenção.

Janela de backup: O intervalo de tempo diário durante o qual o backup será iniciado. É recomendável escolher um período de baixa atividade.

Período de retenção: Por quantos dias os backups serão mantidos. O padrão é 7 dias, mas você pode estendê-lo até 35 dias.



docs.oracle.com
Para um DB System existente:

Acesse o Console do OCI.

Navegue até Bancos de Dados > MySQL HeatWave.

Selecione seu DB System.

Na página de detalhes do DB System, no menu Recursos, clique em Backups.

Clique em Configurar Backups para ajustar a janela de backup ou o período de retenção.



www.oracle.com
2.2. Visualizando Backups Automáticos
Todos os backups, sejam eles automáticos ou manuais, são listados na seção Backups do seu DB System. Você pode identificar backups automáticos pela sua descrição ou pelo fato de serem criados regularmente de acordo com sua janela programada.

3. Backups Manuais (Sob Demanda)
Backups manuais são snapshots completos do seu DB System em um momento específico. Eles são ideais para capturar o estado do banco de dados antes de executar operações de risco (como migrações, grandes atualizações de esquema ou exclusão de dados em massa) ou para criar um ponto de recuperação que você sabe que precisará por um período mais longo do que o período de retenção automático.

3.1. Criando um Backup Manual
Acesse o Console do OCI.

Navegue até Bancos de Dados > MySQL HeatWave.

Selecione seu DB System.

Na página de detalhes do DB System, no menu Recursos, clique em Backups.

Clique no botão Criar Backup Manual.

Forneça uma descrição para o backup. Isso ajuda a identificar o backup posteriormente.

Clique em Criar Backup Manual.



www.oracle.com
O status do backup será exibido na tabela de backups. Pode levar algum tempo para que o backup seja concluído, dependendo do tamanho do seu DB System.

4. Restauração de um DB System
A restauração de um DB System MySQL HeatWave cria um novo DB System a partir de um backup existente. Você não pode restaurar para um DB System existente; em vez disso, um novo DB System é provisionado com os dados do ponto de restauração.

4.1. Opções de Restauração
Restaurar de um Backup Específico: Escolha um backup automático ou manual da lista para restaurar o DB System para o estado em que estava no momento desse backup.

Restaurar para um Ponto no Tempo (Point-in-Time Recovery - PITR): Restaure seu DB System para qualquer ponto no tempo dentro do seu período de retenção de backup (geralmente entre o primeiro backup e a última transação antes da falha). Isso utiliza uma combinação do último backup completo e logs binários para recriar o estado exato.

4.2. Processo de Restauração
Acesse o Console do OCI.

Navegue até Bancos de Dados > MySQL HeatWave.

Você tem duas maneiras de iniciar uma restauração:

Da Lista de Backups:

Selecione seu DB System.

No menu Recursos, clique em Backups.

Localize o backup a partir do qual deseja restaurar (automático ou manual).

Clique no menu Ações (três pontos) ao lado do backup e selecione Restaurar DB System.

Da Página de Detalhes do DB System (para PITR ou o último backup):

Na página de detalhes do DB System, clique no botão Restaurar para Ponto no Tempo.

Você pode então escolher um backup específico ou um ponto no tempo.

Você será solicitado a configurar o novo DB System que será criado. Isso inclui:

Nome de exibição: Um nome para o novo DB System.

Senha do Administrador: Defina uma nova senha para o usuário admin.

VCN e Sub-rede: Selecione a VCN e a sub-rede onde o novo DB System será implantado. É recomendável usar a mesma VCN/Sub-rede que o original, ou uma com conectividade apropriada.

Formato: O formato do novo DB System (pode ser o mesmo ou diferente do original).

Configurações de Backup: Você pode definir novas configurações de backup automático para o DB System restaurado.

Clique em Restaurar DB System.

Um novo DB System será provisionado com os dados do backup selecionado ou do ponto no tempo. O DB System original não será afetado.

5. Melhores Práticas de Backup
Período de Retenção Adequado: Defina um período de retenção de backup automático que atenda aos seus requisitos de recuperação e conformidade.

Backups Manuais Estratégicos: Crie backups manuais antes de grandes mudanças ou eventos importantes para ter pontos de recuperação conhecidos.

Testes de Restauração: Periodicamente, realize restaurações de teste para garantir que seus backups sejam válidos e que você esteja familiarizado com o processo. Isso é vital para um plano de recuperação de desastres eficaz.

Monitoramento de Backups: Monitore o status dos seus backups no console do OCI e configure alarmes para ser notificado sobre falhas de backup.

Entenda o Impacto da Restauração: Lembre-se de que a restauração cria um novo DB System. Planeje como você redirecionará suas aplicações para o novo DB System após a restauração.

Conclusão
O recurso de backup e restauração do MySQL HeatWave no OCI é uma ferramenta poderosa para proteger seus dados e garantir a continuidade dos negócios. Ao configurar backups automáticos, realizar backups manuais quando necessário e entender o processo de restauração, você pode manter seus dados seguros e prontos para recuperação em qualquer situação.