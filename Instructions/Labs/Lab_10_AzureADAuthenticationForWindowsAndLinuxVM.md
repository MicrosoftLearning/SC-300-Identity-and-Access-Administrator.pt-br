---
lab:
  title: '10: autenticação do Azure AD para máquinas virtuais do Windows e do Linux'
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# Laboratório 10: autenticação do Azure AD para máquinas virtuais do Windows e do Linux

**Observação** - Este laboratório requer um Azure Pass. Consulte o laboratório 00 para obter instruções.

## Cenário do laboratório

A empresa decidiu que o Azure Active Directory deve ser usado para fazer logon em máquinas virtuais para acesso remoto.  Este laboratório mostrará como isso pode ser configurado para máquinas virtuais do Windows e do Linux.

#### Tempo previsto: 30 minutos

### Exercício 1: fazer logon em máquinas virtuais do Windows no Azure com o Azure AD

#### Tarefa 1: criar uma máquina virtual do Windows com o logon do Azure AD habilitado

1. Navegue até [https://portal.azure.com](https://portal.azure.com)

1. Selecione **+ Criar um recurso**.

1. Digite **Windows Server** na barra de pesquisa Pesquisar no Marketplace.

1. Selecione **Windows Server** e escolha **Windows Server 2022 Datacenter** na lista suspensa Selecionar um plano de software.

1. Você precisará criar um nome de usuário administrador e uma senha para a VM na guia Básico.
   - Use um nome de usuário que você se lembre e uma senha segura.

1. Na guia **Gerenciamento**, marque a caixa para Fazer logon com o Azure AD na seção Azure AD.

1. Você notará que a **Identidade gerenciada atribuída ao sistema** na seção Identidade é verificada automaticamente e ficará cinza. Essa ação deverá ocorrer automaticamente depois que você habilitar a opção Logon com o Azure AD.

1. Percorra o restante da experiência de criação de uma máquina virtual. 

1. Selecione Criar.

#### Tarefa 2: logon do Azure AD para máquinas virtuais do Azure existentes

1. Navegue até **Máquinas virtuais** no [https://portal.azure.com](https://portal.azure.com).

1. Selecione a máquina virtual recém-criada na Tarefa 1.

1. Selecione **IAM (Controle de acesso)** .

1. Selecione **+ Adicionar** e, em seguida, **Adicionar atribuição de função** para abrir a página Adicionar atribuição de função.

1. Atribua as seguintes configurações:
    - **Tipo de atribuição**: funções de trabalho
    - **Função**: logon de administrador da máquina virtual
    - **Membros**: selecione Usuário, grupo ou entidade de serviço.  Em seguida, use **+ Selecionar membros** para adicionar **Joni Sherman** como um usuário específico para a VM.

1. Selecione **Examinar + atribuir** duas vezes para concluir o processo

#### Tarefa 3: atualizar a VM do servidor para dar suporte ao logon do Azure AD

1. Selecione o item de menu **Conectar**.

1. Na guia **RDP**, selecione **Baixar arquivo RDP**.  Se solicitado, escolha a opção **Manter** para o arquivo.  Ele será salvo na sua pasta Downloads.

1. Abra a pasta **Downloads** no Gerenciador de arquivos.

1. Abra o RDP.

1. Escolha fazer logon como Usuário alternativo.

1. Use o nome de usuário do Administrador e a senha que você cria ao configurar a máquina virtual.
   - Se solicitado, diga sim para permitir o acesso à máquina virtual ou à sessão do RDP.

1. Aguarde até que o servidor esteja aberto e todo o software seja carregado, como o Painel do gerenciador do servidor.

1. Selecione o **botão Iniciar** na máquina virtual.

1. Digite **Painel de controle** e inicie o aplicativo do painel de controle.

1. Selecione **Sistema e segurança** na lista de configurações.

1. Na configuração **Sistema**, selecione a opção **Permitir acesso remoto**.

1. Na parte inferior da caixa de diálogo que se abre, você verá uma seção **Área de trabalho remota**.

1. **Desmarque** a caixa **Permitir conexões somente de computadores que executam a Área de trabalho remota com a Autenticação em nível de rede**.

1. Selecione **Aplicar** e, em seguida, **OK**.

1. **Saia** da sessão RDP da máquina virtual.


#### Tarefa 4: modificar seu arquivo RDP para dar suporte ao logon do Azure AD

1. Abra a pasta **Downloads** no Gerenciador de arquivos.

1. **Faça uma cópia** do arquivo RDP e adicione **-AzureAD** ao final do nome do arquivo.

1. Edite a nova versão do arquivo RDP que você acabou de copiar usando o Bloco de notas. Adicione estas duas linhas de texto à parte inferior do arquivo:
     ```
        enablecredsspsupport:i:0
        authentication level:i:2
     ```
 
 1. **Salve** o arquivo RDP.  Agora você deve ter duas versões do arquivo:
      - <<virtual machine name>>.RDP
      - <<virtual machine name>>-AzureAD.RDP

#### Tarefa 5: conectar-se ao Windows Server 2022 Datacenter usando o logon do Azure AD

1. Abra o **<<virtual machine name>>-AzureAD.RDP

1. Selecione **Conectar** quando a caixa de diálogo for aberta.

1. Em vez de receber uma solicitação sobre qual conta de usuário usar para fazer logon, você deve receber uma mensagem perguntando se deseja se conectar ao computador remoto.

1. Selecione **Sim** na parte inferior da tela.

1. A sessão de Área de trabalho remota deve abrir e mostrar a tela de logon do Windows Server.  **Outro usuário** com um botão OK deve ser exibido.

1. Selecione **OK**.

1. Na caixa de diálogo de logon, insira as seguintes informações:
   - Nome de usuário = **AzureAD\JoniS@<<your lab domainname>>
   - Senha = Insira a senha fornecida pelo provedor do laboratório

   OBSERVAÇÃO: JoniS é o usuário que concedemos acesso para fazer logon como administrador durante a Tarefa 1.

1. O Windows Server deve confirmar o logon e abrir o painel normal do Gerenciador do servidor.

#### Tarefa 6: teste opcional para explorar o logon do Azure AD

1. Verifique se o JoniS foi o único usuário adicionado ao grupo Administradores.

1. No painel do Gerenciador do servidor, selecione o menu **Ferramentas** no canto superior esquerdo.

1. Inicie a ferramenta **Gerenciamento do computador**.

1. Abra **Usuários e grupos locais** e navegue até **Grupos, Administradores**.

1. Você deve ver **Azure\JoniSherman....** na lista.

1. Verifique se outros membros do Azure AD podem fazer logon.

1. Saia da sessão de área de trabalho remota.

1. Inicie o arquivo **<<server name>>-AzureAD.RDP** novamente.

1. Tente fazer logon como outros membros do Azure AD, como AdeleV, AlexW ou DiegoS.

1. Observe que o acesso a cada um desses usuários é negado.

### Exercício opcional 2: fazer logon em máquinas virtuais do Linux no Azure com o Azure AD

#### Tarefa 1: criar uma VM do Linux com a identidade gerenciada atribuída ao sistema

1. Navegue até [https://portal.azure.com](https://portal.azure.com)

1. Selecione **+ Criar um recurso**.

1. Selecione **Criar** em **Ubuntu Server 18.04 LTS** na exibição Popular.

1. Na guia **Gerenciamento**, marque a caixa para habilitar o logon com o **Azure Active Directory (Visualização)**.

1. Certifique-se de que **Identidade gerenciada atribuída pelo sistema** está selecionada.

1. Percorra o restante da experiência de criação de uma máquina virtual. Durante esta visualização, você terá que criar uma conta de administrador com nome de usuário e senha ou chave pública SSH.

#### Tarefa 2: logon do Azure AD para máquinas virtuais do Azure existentes

1. Navegue até **Máquinas virtuais** no [https://portal.azure.com](https://portal.azure.com).

1. Selecione **IAM (Controle de acesso)** .

1. Selecione Adicionar > Adicionar atribuição de função para abrir a página Adicionar atribuição de função.

1. Atribua a função a seguir. 
    - **Função**: logon de Administrador da máquina virtual ou logon de Usuário da máquina virtual
    - **Atribuir acesso a**: usuário, grupo entidade de serviço ou identidade gerenciada

1. Para ver as etapas detalhadas, confira Atribuir funções do Azure usando o portal do Azure.
