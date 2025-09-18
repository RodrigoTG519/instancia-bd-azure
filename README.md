# instancia-bd-azure

Este repositório tem como finalidade apresentar um passo a passo de como fazer uma instância de Banco de dados na plataforma azure da microsoft

Antes de começarmos com o passo a passo teremos que ver alguns pré-requisitos.

- Ter uma assinatura azure, se não tiver crie uma conta gratuita;
- Ter a permissão necessária sobre o recurso. Ex: Contribuidor de Instância Gerenciada);
- Verificar se na Regiâo de escolha suporta Instâncias;
- Verificar se tem uma rede virtual ou uma sub-rede para hospedar a instância, se não tiver terá que criar uma;

Como criar uma Instância Gerenciada:
- Faça login com a sua conta no portal Azure;
- No Menu lateral esquerdo clique em SQL do Azure. Se não encontrar, vá em todos os serviços e procure por "SQL do Azure".
- Dentro do SQL do Azure, escolha +Criar para abrir as opções de implementação da instância;
- Selecione "Instâncias Gerenciadas de SQL" como tipo de implementação;
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Agora um passo a passo de configurações essenciais da instância.

Básico:
- Assinatura: Escolha a assinatura de preferência;
- Grupo de recursos: Crie um novo ou use um já existente;
- Nome da Instância: Coloque um nome que siga as regras de nomeclatura;
- Região: Escolha a região que ela será provisionada;
- Autenticação: Escolha a opção que estiver mais confortável seja ela SQL ou Microsoft Entra ou até ambas;
- Login de ADM da instância: Nome de usuário do administrador;
- Senha: Faça uma senha que atenda os requisitos(complexidade, tamanho mínimo, etc...);
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Computação + Armazenamento:
- Camada de Serviço: Escolha a de prefêrencia, mas a de Uso Geral já funciona normalmente;
- Geração de Hardware: O padrão é o Gen 5, essa opção vai limitar o computador e sua memória;
- vCores: Representa a quantidade de recursos que seram utilizados. Oito vCores é o padrão;
- Armazenamento de GB: Escolha baseado no tamanho de dados que serão colocados;
- Modelo de licença: Se tiver como escolher a opção "pagar conforme o uso", escolha ela;
- Redundância de Backup: O armazenamento de backup com redundância geográfica é o padrão e o recomendado;
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Rede:
- Rede virtual/sub-rede: Crie ou use uma rede virtual existente;
- Tipo de conexão: Pode ser entre redes do Azure, Internet Pública ou limitar ao virtual network. Redirecionar é o recomendado;
- Ponto de extremidade público: Selecionar Desabilitar;
- Se o ponto de extremidade estiver habilitado escolha uma dessas opções:
  -Serviços Azure: Essa opção é recomendada se o usuário for conectar usando power BI ou outro serviço multilocatário;
  -Internet: Utilizada para testes e criação rápida de uma instância. Não é recomendada para ambientes de produção;
  -Sem acesso: Essa opção cria regras de seguranças que o administrador pode modificar para tormar a instância acessível;
Se foi selecionado Desabilitar pode ignorar as opções acima;
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Configurações Adicionais:
- Ordenação: Escolha a ordenação que desejar;
- Fuso Horário: Selecione o fuso horário que vai estar na instância;
- Replicação Geográfica: Selecione Não. Habilite somente se for usar a instância como um grupo de failover secundário;
- Janela de Manutencão: Faça um agendamento adequado para sua instância quando for mantida pelo serviço;
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Marcas(Tags):
Defina marcações para ter uma melhor organização do recurso, por exemplo indicar o ambiente como produção/desenvolvimento, indicar também o proprietário, etc....
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Por fim clique em Revisar+Criar para revisar suas escolhas e se estiver tudo certo clique em Criar para iniciar o provisionamento o que pode demorar.
Depois de concluir vá ao grupo de recursos para ver o que acabou de criar.

Agora que a Instância está criada teremos que criar o banco de dados dentro dessa instância que foi criada. para isso apenas siga esse passo a passo.

- No portal, acesse a instância que foi criada;
- Clique em + Novo banco de dados da instância;
- Defina um nome para o banco de dados;
- Na opção origem seleciona vazio para ter um banco de dados sem nenhum dado ou restaure um a partir do backup;
- defina tamanho;
- Revise e depois Criar;
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Para conectar-se depois:
  -Vá à página de Visão Geral da instância no Portal para encontrar o Host / FQDN (nome de domínio totalmente qualificado) que você usará para conexão. 
  -Use esse FQDN + credenciais de administrador + porta padrão para conexões SQL.

Depois de todos esses passos o Banco de Dados estará pronto para uso...
