Guia Completo: Alta Disponibilidade (HA) em MySQL HeatWave
O MySQL HeatWave é um serviço de banco de dados na nuvem totalmente gerenciado pela Oracle, que combina o MySQL com um acelerador de consulta em memória (HeatWave) para cargas de trabalho de OLTP (processamento de transações online), OLAP (processamento analítico online) e aprendizado de máquina. A alta disponibilidade é um recurso crítico no HeatWave para garantir que suas aplicações permaneçam operacionais e seus dados acessíveis, mesmo diante de falhas.

O que é Alta Disponibilidade no MySQL HeatWave?
No contexto do MySQL HeatWave, a Alta Disponibilidade (HA) refere-se à capacidade do serviço de manter as instâncias do banco de dados e os clusters HeatWave disponíveis e operacionais, minimizando o tempo de inatividade. Isso é alcançado através de uma arquitetura redundante e mecanismos automáticos de failover.

Principais Características de HA no MySQL HeatWave:
Arquitetura Tripla Instância: Um sistema de banco de dados de alta disponibilidade no MySQL HeatWave é composto por três instâncias MySQL: uma instância primária (leitura/escrita) e duas instâncias secundárias.

Replicação de Grupo MySQL (MySQL Group Replication): Os dados são replicados da instância primária para as instâncias secundárias usando a replicação de grupo do MySQL. Esta é uma forma de replicação síncrona/semi-síncrona que garante consistência de dados e zero perda de dados em caso de falha da instância primária.

Distribuição entre Zonas de Disponibilidade (AZs) / Domínios de Falha (FDs): Para resiliência máxima, as três instâncias MySQL são colocadas em diferentes zonas de disponibilidade (em regiões multi-AZ) ou em domínios de falha distintos dentro da mesma AZ (em regiões single-AZ). Isso protege contra falhas de hardware, rede ou energia que afetam uma AZ ou FD específica.

Failover Automático: Em caso de falha da instância primária, o serviço HeatWave automaticamente promove uma das instâncias secundárias para funcionar como a nova instância primária. Este processo é projetado para ser rápido, garantindo a retomada da disponibilidade para as aplicações cliente sem perda de dados.

Switchover: Além do failover automático, o HeatWave Service permite que você promova manualmente uma das instâncias secundárias como a instância primária (um "switchover"). Isso é útil para manutenção planejada ou atualizações.

Recuperação do Cluster HeatWave: Se a instância primária do DB System falhar e uma nova primária for promovida em uma AZ/FD diferente, o cluster HeatWave pode ser recriado e os dados automaticamente recuperados da camada de armazenamento ou recarregados do novo DB System. Em cenários onde a nova primária está na mesma AZ/FD, o cluster HeatWave existente pode ser reutilizado.



severalnines.com
Como a Alta Disponibilidade é Conquistada?
A HA no MySQL HeatWave é uma funcionalidade gerenciada que abstrai grande parte da complexidade de configurar e manter um cluster de alta disponibilidade.

Criação do DB System HA: Ao criar um MySQL DB System no Oracle Cloud Infrastructure (OCI) ou outras nuvens suportadas (AWS, Azure), você seleciona a opção de Alta Disponibilidade. Isso provisiona automaticamente as três instâncias MySQL e configura a replicação.

Monitoramento Contínuo: O serviço HeatWave monitora constantemente a saúde da instância primária. Ele usa mecanismos internos para detectar falhas e iniciar o processo de failover.

Endereço IP Virtual (VIP): Embora não explicitamente detalhado para o usuário, o serviço gerencia um endpoint de conexão que sempre aponta para a instância primária ativa, tornando o failover transparente para as aplicações. As aplicações se conectam a um único endpoint, e o serviço redireciona as conexões para a instância primária ativa.

Consistência de Dados: A Replicação de Grupo MySQL garante que todas as transações confirmadas na instância primária sejam replicadas para as secundárias antes que o failover ocorra, prevenindo a perda de dados.

Gerenciamento do HeatWave Cluster: O cluster HeatWave (o componente de análise em memória) está sempre anexado à instância primária do DB System. Em caso de failover, o serviço gerencia o desanexamento do cluster da antiga primária e o reanexamento ou recriação do cluster na nova primária.

Vantagens da HA no MySQL HeatWave
Zero Perda de Dados: Graças à replicação de grupo, o MySQL HeatWave garante zero perda de dados durante o failover.

Tempo de Inatividade Mínimo: O processo de failover é rápido e automático, minimizando o impacto nas operações da sua aplicação.

Simplicidade: A complexidade da configuração de HA é gerenciada pelo serviço, permitindo que os usuários se concentrem no desenvolvimento de aplicações.

Resiliência a Falhas: Protege contra uma ampla gama de falhas, incluindo falhas de instância, zona de disponibilidade ou domínio de falha.

SLA Garantido: A Oracle oferece um Acordo de Nível de Serviço (SLA) para a disponibilidade do MySQL HeatWave, geralmente com alta porcentagem de tempo de atividade (ex: 99.99%).

Considerações e Limitações
Custo: Sistemas de HA consomem mais recursos (CPU, RAM, armazenamento) do que sistemas standalone, refletindo-se em um custo maior.

Latência de Escrita: As transações de escrita podem ter uma latência ligeiramente maior em sistemas HA devido à necessidade de coordenação e aprovação por múltiplas instâncias na replicação de grupo.

Acesso: Você só tem acesso de leitura/escrita à instância primária. As instâncias secundárias não são acessíveis diretamente por clientes externos.

Manutenção: A manutenção de um DB System HA (como upgrades) é realizada através de atualizações progressivas, que podem envolver um breve período de inatividade antes que a nova instância promovida retome as conexões.

Pré-requisitos: Para habilitar HA em um DB System standalone existente, pode ser necessário atender a certos pré-requisitos, como ter chaves primárias em todas as tabelas e não ter clusters HeatWave anexados temporariamente durante a transição.

Conclusão
A Alta Disponibilidade é um pilar fundamental do MySQL HeatWave, projetada para garantir que seus dados críticos e suas aplicações permaneçam disponíveis e resilientes a falhas. Ao alavancar a arquitetura de três instâncias, a Replicação de Grupo MySQL e o gerenciamento automatizado de failover, o HeatWave oferece uma solução de banco de dados robusta para cargas de trabalho que exigem alta disponibilidade e consistência de dados.