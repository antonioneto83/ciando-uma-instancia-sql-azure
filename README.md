# ciando-uma-instancia-sql-azure

Este guia de início rápido ensina você a criar uma implantação da Instância Gerenciada de SQL do Azure usando o portal do Azure, o PowerShell e a CLI do Azure.

Observação

Experimente a Instância Gerenciada de SQL do Azure sem custo e obtenha 720 horas de vCore em uma Instância Gerenciada de SQL de Uso Geral com até 100 bancos de dados por instância nos primeiros 12 meses.
Pré-requisitos

Para criar uma instância gerenciada de SQL, você precisa dos seguintes pré-requisitos:

    Uma assinatura do Azure. Se você não tem uma assinatura do Azure, crie uma conta gratuita
    No caso geral, seu usuário precisa ter a função SQL Managed Instance Contributor atribuída no âmbito da assinatura.
    Se o provisionamento for em uma sub-rede que já está delegada à Instância Gerenciada do Azure SQL, o seu usuário só precisará da permissão Microsoft.Sql/managedInstances/write atribuída em nível de escopo de assinatura.
    O módulo Az.SQL mais recente para a versão atual do PowerShell ou a versão mais recente da CLI do Azure.

Para obter as limitações, confira Regiões compatíveis e Tipos de assinatura compatíveis.
Criar uma Instância Gerenciada de SQL do Azure

Você pode criar uma implantação de Instância Gerenciada de SQL do Azure usando o portal do Azure, o PowerShell ou a CLI do Azure.

Considere o seguinte:

    Cancele o processo de provisionamento por meio do portal do Azure, do PowerShell, da CLI do Azure ou de outras ferramentas usando a API REST.
    A implantação da instância será atrasada se for afetada por outras operações na mesma sub-rede, como uma restauração de longa duração ou o dimensionamento de uma instância.
    As permissões de leitura do grupo de recursos são necessárias para visualizar a instância gerenciada do SQL no seu grupo de recursos.

Importante

Para a duração da operação de criação, consulte as durações da operação de gerenciamento.

    Portal
    PowerShell
    CLI do Azure

Entre no Portal do Azure

Para criar sua instância no portal do Azure, primeiro você precisará entrar no portal do Azure e preencher as informações na página Criar Instância Gerenciada de SQL do Azure.

Para sua instância, siga estas etapas:

    Entre no portal do Azure.

    Vá para o Hub SQL do Azure em aka.ms/azuresqlhub.

    No painel da Instância Gerenciada de SQL do Azure, selecione Mostrar opções.

    Na janela de opções da Instância Gerenciada de SQL do Azure , selecione Criar Instância Gerenciada de SQL.

    Captura de tela do portal do Azure do Hub SQL do Azure, mostrando o botão Mostrar opções e o botão Criar Instância Gerenciada de SQL.

Guia Básico

Preencha as informações obrigatórias exigidas na guia Básico, que é o requisito mínimo para provisionar uma Instância Gerenciada de SQL.

A tabela a seguir fornece detalhes para as informações necessárias na guia Básico:
Configuração 	Valor sugerido 	Description
Assinatura 	Sua assinatura. 	Uma assinatura que concede a você permissão para criar recursos.
Grupo de recursos 	Um grupo de recursos novo ou existente. 	Para ver os nomes do grupo de recursos válidos, consulte Regras e restrições de nomenclatura.
Nome da instância gerenciada 	Qualquer nome válido. 	Para ver os nomes válidos, consulte Regras e restrições de nomenclatura.
Região 	A região na qual você deseja criar a instância gerenciada de SQL. 	Para obter mais informações sobre as regiões, confira Regiões do Azure.
Pertence a um pool de instâncias? 	Selecione Sim para que essa instância seja criada dentro de um pool de instâncias. 	
Método de autenticação 	Usar a autenticação do SQL 	Para este início rápido, use a autenticação SQL. Mas, para melhorar a segurança, use a autenticação do Microsoft Entra .
Logon de administrador da Instância Gerenciada 	Qualquer nome de usuário válido. 	Para ver os nomes válidos, consulte Regras e restrições de nomenclatura. Não use serveradmin, pois essa é uma função reservada no nível de servidor.
Senha 	Qualquer senha válida. 	A senha deve ter no mínimo 16 caracteres e atender a requisitos de complexidade definidos.

Em Detalhes da instância gerenciada, selecione Configurar instância gerenciada na seção Computação + armazenamento para abrir a página Computação + armazenamento.

Captura de tela da página Criar Instância Gerenciada de SQL do Azure com a opção Configurar Instância Gerenciada selecionada.

A tabela a seguir fornece recomendações para a computação e o armazenamento para sua instância gerenciada SQL de exemplo:
Configuração 	Valor sugerido 	Description
Camada de Serviço 	Uso Geral 	A camada Uso Geral atende à maioria das cargas de trabalho de produção e é a opção padrão. A camada de serviço Uso Geral de Última Geração aprimorada também é uma ótima escolha para a maioria das cargas de trabalho. Para saber mais, consulte limites de recursos.
Geração do hardware 	Série Standard (Gen 5) 	A série Standard (Gen5) é a geração de hardware padrão, que define os limites de computação e de memória. A série Standard (Gen5) é o padrão.
vCores 	Designe um valor. 	Os vCores representam a quantidade exata de recursos de computação que sempre são provisionados para a carga de trabalho. Oito vCores é o padrão.
Armazenamento em GB 	Designe um valor. 	Tamanho do armazenamento em GB. Selecione-o com base no tamanho de dados esperado.
Licença do SQL Server 	Selecione o modelo de licenciamento aplicável. 	Use o pagamento conforme o uso, uma licença SQL existente com o Benefício Híbrido do Azure ou habilite os direitos de failover híbrido
Redundância do armazenamento de backup 	Armazenamento de backup com redundância geográfica. 	Redundância de armazenamento dentro do Azure para o armazenamento de backup. O armazenamento de backup com redundância geográfica é o padrão e o recomendado, embora a redundância local e de zona geográfica permita maior flexibilidade de custo e residência de dados de região única.

Depois de designar sua configuração de Computação + Armazenamento, use Aplicar para salvar suas configurações e navegar de volta para a página Criar Instância Gerenciada SQL do Azure. Selecione Próximo para ir para a guia Rede
Guia Rede

Preencha informações opcionais na guia Rede . Se você omitir essas informações, o portal aplicará as configurações padrão.

A tabela a seguir fornece detalhes para obter informações na guia Rede:
Configuração 	Valor sugerido 	Description
Rede virtual / sub-rede 	Crie ou use uma rede virtual existente. 	Se uma rede ou sub-rede não estiver disponível, ela deverá ser modificada para atender aos requisitos de rede antes de selecioná-la como um destino para a nova instância gerenciada de SQL.
Tipo de conexão 	Escolha um tipo de conexão adequado. 	Para obter mais informações, confira os tipos de conexão.
Ponto de extremidade público 	Selecione Desabilitar. 	Para que a instância gerenciada de SQL fique acessível por meio do ponto de extremidade de dados público, será necessário habilitar essa opção.
Permitir o acesso de (se o Ponto de extremidade público estiver habilitado) 	Selecione Sem Acesso 	O portal configura o grupo de segurança com um ponto de extremidade público.

De acordo com a situação, selecione uma das seguintes opções:

    Serviços do Azure: recomendamos essa opção quando você estiver se conectando de Power BI ou de outro serviço multilocatário.
    Internet: use para fins de teste quando quiser criar rapidamente uma instância gerenciada de SQL. Não recomendado para ambientes de produção.
    Sem acesso: esta opção cria a regra de segurança Negar. Modifique essa regra para tornar uma instância gerenciada de SQL acessível por meio de um ponto de extremidade público.


Para obter mais informações sobre segurança de ponto de extremidade público, consulte Usar a Instância Gerenciada de SQL do Azure com segurança com pontos de extremidade públicos.

Selecione Examinar + criar para examinar suas escolhas antes de criar uma instância gerenciada de SQL. Ou defina as configurações de segurança selecionando Avançar: Configurações de segurança.
Guia Segurança

Para este início rápido, deixe as configurações na guia Segurança em seus valores padrão.

Selecione Examinar + criar para examinar suas escolhas antes de criar uma instância gerenciada de SQL. Ou defina mais configurações personalizadas selecionando Avançar: configurações adicionais.
Configurações adicionais

Preencha as informações opcionais na guia Configurações adicionais. Se você omitir essas informações, o portal aplicará as configurações padrão.

A tabela a seguir oferece detalhes sobre as informações na guia Configurações adicionais:
Configuração 	Valor sugerido 	Description
Ordenação 	Escolha a ordenação que você deseja usar para sua instância gerenciada de SQL. Se estiver migrando bancos de dados do SQL Server, verifique a ordenação de origem usando SELECT SERVERPROPERTY(N'Collation') e use esse valor. 	Para obter informações sobre ordenações, confira Definir ou alterar a ordenação do servidor.
Fuso horário 	Selecione o fuso horário observado pela instância gerenciada de SQL. 	Para obter mais informações, consulte Fusos horários na Instância Gerenciada de SQL do Azure.
Replicação geográfica 	Selecione Não. 	Habilite essa opção somente se você planeja usar a instância gerenciada de SQL como um grupo de failover secundário.
Janela de manutenção 	Escolha uma janela de manutenção adequada. 	Designe um agendamento para quando sua instância for mantida pelo serviço.

Selecione Examinar + criar para examinar suas escolhas antes de criar uma instância gerenciada de SQL. Ou, então, configure as marcas do Azure selecionando Avançar: Marcas (recomendado).
Marcações

Adicione marcas aos recursos no modelo do ARM (modelo do Azure Resource Manager). As marcas ajudam você a organizar logicamente seus recursos. Os valores de marca são mostrados nos relatórios de custo e permitem outras atividades de gerenciamento por marca. Considere pelo menos marcar sua nova instância gerenciada de SQL com a marca Proprietário para identificar quem criou e a marca Ambiente para identificar se esse sistema é Produção, Desenvolvimento etc. Para obter mais informações, consulte Desenvolver sua estratégia de nomenclatura e marcação para recursos do Azure.

Selecione Examinar + criar para prosseguir.
Examinar + criar

Na guia Revisar + criar , examine suas escolhas e selecione Criar para implantar sua instância gerenciada de SQL.
Monitorar o progresso da implantação

    Selecione o ícone Notificações para exibir o status da implantação.

    Captura de tela do progresso da implantação de uma implantação de Instância Gerenciada de SQL.

    Selecione Implantação em andamento na notificação para abrir a janela da Instância Gerenciada de SQL e monitorar mais detalhadamente o progresso da implantação.

Depois que a implantação for concluída, navegue até o grupo de recursos para exibir sua instância gerenciada de SQL:

Captura de tela dos recursos da Instância Gerenciada de SQL no portal do Azure.

Dica

Se você fechou o navegador da Web ou se afastou da tela de progresso da implantação, poderá monitorar a operação de provisionamento por meio da página Visão geral da instância gerenciada de SQL no portal do Azure, no PowerShell ou na CLI do Azure.
Revisar configurações de rede

Selecione o recurso Tabela de rotas em seu grupo de recursos para examinar o objeto padrão de tabela de rotas definido pelo usuário e as entradas para rotear o tráfego de e dentro da rede virtual da Instância Gerenciada de SQL. Para alterar ou adicionar rotas, abra Rotas nas configurações da tabela de rotas.

Selecione o objeto do Grupo de segurança de rede para examinar as regras de segurança de entrada e saída. Para alterar ou adicionar regras, abra Regras de Segurança de Entrada e Regras de Segurança de Saída nas configurações do grupo de segurança de rede.

Captura de tela das Regras de Segurança para sua instância no portal do Azure.

Importante

Se você tiver habilitado o ponto de extremidade público para a Instância Gerenciada de SQL, abra as portas para permitir conexões do tráfego de rede com a Instância Gerenciada de SQL vindo da Internet pública.
Criar banco de dados

Você pode criar um novo banco de dados usando o portal do Azure, o PowerShell ou a CLI do Azure.

    Portal
    PowerShell
    CLI do Azure

Para criar um novo banco de dados para a sua instância no portal do Azure, siga estas etapas:

    Acesse a Instância Gerenciada de SQL no portal do Azure.

    Na página Visão geral, escolha + Novo banco de dados da sua instância gerenciada de SQL para abrir a página Criar banco de dados gerenciado do SQL do Azure.

    Captura de tela da criação de um novo banco de dados no portal do Azure.

    Dê um nome para o banco de dados na guia Básico.

    Na guia Fonte de dados, selecione Nenhuma para um banco de dados vazio ou restaure um banco de dados a partir do backup.

    Defina as configurações restantes nas guias restantes e selecione Revisar + criar para validar suas escolhas.

    Use Criar para implantar seu banco de dados.

Recuperar detalhes da conexão para a Instância Gerenciada de SQL

Para se conectar à Instância Gerenciada de SQL, siga estas etapas para recuperar o nome do host e o FQDN (nome de domínio totalmente qualificado):

    Volte ao grupo de recursos e escolha o objeto de instância gerenciada de SQL que foi criado.

    Na guia Visão Geral, localize a propriedade Host. Copie o nome do host para a área de transferência da instância gerenciada do SQL para uso no próximo início rápido selecionando o botão Copiar para área de transferência .

    Captura de tela da página de Visão Geral para a instância no portal do Azure com o nome do host selecionado.

    O valor copiado representa um FQDN (nome de domínio totalmente qualificado) que pode ser usado para se conectar à Instância Gerenciada de SQL. É semelhante ao seguinte exemplo de endereço: your_host_name.a1b2c3d4e5f6.database.windows.net.
