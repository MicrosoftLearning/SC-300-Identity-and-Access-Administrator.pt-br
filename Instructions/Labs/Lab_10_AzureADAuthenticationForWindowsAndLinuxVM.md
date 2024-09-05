---
lab:
  title: 10 - Autenticação do Microsoft Entra ID para Máquinas Virtuais do Windows e Linux
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# Laboratório 10: Autenticação do Microsoft Entra para máquinas virtuais do Windows e Linux

**Observação** – Este laboratório requer um Azure Pass. Consulte o laboratório 00 para obter instruções.

## Cenário do laboratório

A empresa decidiu que o Microsoft Entra ID deve ser usado para fazer logon em máquinas virtuais para acesso remoto.  Este laboratório mostrará como isso pode ser configurado para máquinas virtuais Windows e Linux.

#### Tempo estimado: 30 minutos

### Exercício 1: Fazer logon em Máquinas Virtuais do Windows no Azure com o Microsoft Entra ID

#### Tarefa 1: Criar uma Máquina Virtual do Windows com o logon do Microsoft Entra ID habilitado

1. Navegue para o [https://portal.azure.com](https://portal.azure.com)

1. Selecione **+ Criar um recurso**.

1. Digite **Windows 11** na barra de pesquisa Pesquisar no Marketplace e aperte **Enter**.

1. Na caixa **Windows 11**, selecione **Criar v** e escolha **Windows 11 Enterprise, versão 22H2** no menu que abrir.

1. Crie a VM usando os seguintes valores na guia **Noções básicas**:
  | Campo | Valor a ser usado |
  | :-- | :-- |
  | Assinatura | Azure Pass – Sponsorship |
  | Grupo de recursos | Criar Novo – rgEntraLogin |
  | Nome da máquina virtual | vmEntraLogin |
  | Region | *padrão* |
  | Opções de disponibilidade | Nenhuma redundância de infraestrutura necessária |
  | Tipo de segurança | Standard |
  | Tamanho | Standard DC1s_v3 - 1 vcpu, 8 GiB de memória |
  | Nome de Usuário do Administrador | vmEntraAdmin |
  | Senha de administrador | Use a fornecida pelo ambiente de laboratório ou crie uma senha segura que você consiga lembrar |
  | Licenciamento | Confirme se você tem uma licença |

1. Você não precisará alterar nada nas guias **Discos** ou **Rede**, mas poderá revisar os valores.

1. Passe para a guia **Gerenciamento**, marque a caixa **Logon com Microsoft Entra ID** na seção Microsoft Entra ID.

        NOTE: You will notice that the **System assigned managed identity** under the Identity section is automatically checked and turned grey. This action should happen automatically once you enable Login with Microsoft Entra ID.

1. Selecione **Examinar + Criar**

1. Depois de selecionar **Criar**.

#### Tarefa 2: Entrar com o Microsoft Entra ID nas Máquinas Virtuais do Azure existentes

1. Navegue até **Máquinas Virtuais** em https://portal.azure.com[](https://portal.azure.com).

1. Selecione uma máquina virtual recentemente criada na Tarefa 1.

1. Selecione **IAM (Controle de acesso)** .

1. Selecione **+ Adicionar**, e depois **Adicionar Atribuição de Função** para abrir a página Adicionar atribuição de função.

1. Atribua as seguintes configurações:
    - **Tipo de atribuição**: funções de trabalho
    - **Função** logon de administrador da máquina virtual
    - **Membros**, selecione Usuário, grupo ou entidade de serviço.  Em seguida, use **+ Selecionar membros** para adicionar **Joni Sherman** como um usuário específico para a VM.

1. Selecione **Revisão + atribuir** para concluir o processo

#### Tarefa 3: Atualizar a VM do servidor para dar suporte ao logon do Microsoft Entra ID

1. No menu **Conectar**, selecione o item **Conectar**.

1. Na guia **RDP**, selecione **Baixar arquivo RDP**.  Se solicitado, escolha a opção **Manter** para o arquivo.  Ele será salvo em sua pasta Downloads.

1. Abra a pasta **Downloads** no Gerenciador de arquivos.

1. Abra o RDP.

1. Escolha fazer logon como Usuário Alternativo.

1. Use o nome de usuário Admin e a Senha que você cria ao configurar a máquina virtual.
   - Se solicitado, diga sim para permitir o acesso à máquina virtual ou à sessão RDP.

1. Aguarde até que a VM seja aberta e todo o software seja carregado.

1. Selecione o **botão Iniciar** na máquina virtual.

1. Digite **Painel de Controle** e inicie o aplicativo do painel de controle.

1. Selecione **Sistema e Segurança** na lista de configurações.

1. Na configuração **Sistema**, selecione a opção **Permitir acesso remoto**.

  OBSERVAÇÃO – você não precisa abrir o submenu Sistema. A opção está disponível no cabeçalho Sistema.

1. Na parte inferior da caixa de diálogo que se abre, você verá uma seção **Área de Trabalho Remota**.

1. **Desmarque** a caixa **Permitir conexões somente de computadores que executam a Área de Trabalho Remota com a Autenticação no Nível da Rede**.

1. Selecione **Aplicar** e, em seguida, **OK**.

1. **Saia** da sessão RDP com a máquina virtual.

#### Tarefa 4 – Modificar o arquivo RDP para dar suporte ao logon do Microsoft Entra ID

1. Abra a pasta **Downloads** no gerenciador de arquivos.

1. **Faça uma cópia** do arquivo RDP e adicione **-EntraID** ao final do nome do arquivo.

1. Edite a nova versão do arquivo RDP que você acabou de copiar usando o Bloco de Notas. Adicione estas duas linhas de texto à parte inferior do arquivo:
     ```
        enablecredsspsupport:i:0
        authentication level:i:2
     ```
 
 1. **Salve** o arquivo RDP.  Agora você deve ter duas versões do arquivo:
      - <<virtual machine name>>.RDP
      - <<virtual machine name>>-EntraID.RDP

#### Tarefa 5 – Conectar-se à máquina virtual do Windows usando o logon do Microsoft Entra ID

1. Abra o **<<virtual machine name>>-EntraID.RDP

1. Selecione **Conectar** quando a caixa de diálogo abrir.

1. Em vez de ser perguntado sobre com qual conta de usuário fazer logon, você deve receber uma mensagem perguntando se deseja se conectar ao computador remoto.

1. Selecione **Sim** na parte inferior da tela.

1. A sessão da Área de Trabalho Remota deve abrir e mostrar a tela de logon do Windows Server.  **Outro usuário** com um botão OK deve ser exibido.

1. Selecione **OK**.

1. Na caixa de diálogo de logon, insira as seguintes informações:
   - Nome de usuário = **AzureAD\JoniS@ seu nome de domínio**
   - Senha = Insira a senha fornecida pelo provedor do laboratório

   NOTA: JoniS é o usuário que concedemos acesso para fazer logon como administrador durante a Tarefa 1.

1. O Windows confirmará o login e abrirá na tela normal.

#### Tarefa 6 – Teste opcional para explorar o logon do Microsoft Entra ID

1. Verifique se o JoniS foi o único usuário adicionado ao grupo Administradores.

1. Use clique secundário do mouse no botão INICIAR e selecione **Gerenciamento do computador** no menu pop-up.

1. Abra **Usuários e Grupos Locais** e navegue até **Grupos, Administradores**.

1. Você deve ver **Azure\JoniSherman...** na lista.

1. Verifique se outros membros do Microsoft Entra ID conseguem entrar.

1. Saia da sessão de Área de Trabalho Remota.

1. Inicie o arquivo **<<server name>>-EntraID.RDP** novamente.

1. Tente fazer login como outros usuários do Microsoft Entra, como AdeleV, AlexW ou DiegoS.

1. Você deve notar que o acesso a cada um desses usuários é negado.

### Exercício Opcional 2 – Fazer logon nas Máquinas Virtuais do Linux no Azure com o Microsoft Entra ID

#### Tarefa 1 – Criar uma VM do Linux com a identidade gerenciada atribuída pelo sistema

1. Navegue para o [https://portal.azure.com](https://portal.azure.com)

1. Selecione **+ Criar um recurso**.

1. Pesquise por **Ubuntu**.

1. Selecione **Criar** em **Ubuntu Server 22.04 LTS**. Você pode usar outros servidores Linux para este laboratório de teste.

1. Na guia **Gerenciamento**, marque a caixa para habilitar o **Logon com o Microsoft Entra ID**.

1. Certifique-se de que **Identidade gerenciada atribuída pelo sistema** está selecionada.

1. Percorra o restante da experiência de criação de uma máquina virtual. Durante esta visualização, você terá que criar uma conta de administrador com nome de usuário e senha ou chave pública SSH.

#### Tarefa 2: Entrar com o Microsoft Entra ID nas Máquinas Virtuais do Azure existentes

1. Navegue até **Máquinas Virtuais** em https://portal.azure.com[](https://portal.azure.com).

1. Selecione **IAM (Controle de acesso)** .

1. Selecione Adicionar > Adicionar atribuição de função para abrir a página Adicionar atribuição de função.

1. Atribua a função a seguir. 
    - **Função**: logon de administrador de máquina virtual ou logon de usuário de máquina virtual
    - **Atribuir acesso a**: usuário, grupo, entidade de serviço ou identidade gerenciada.

1. Para ver as etapas detalhadas, confira Atribuir funções do Azure usando o portal do Azure.
