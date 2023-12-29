---
lab:
  title: 07 - Adicionar identidade híbrida com o Azure AD Connect
  learning path: '01'
  module: Module 01 - Implement an identity management solution
---

# Laboratório 07 (OPCIONAL): adicionar identidade híbrida com o Azure AD Connect

**Observação** - Este laboratório requer um Azure Pass. Consulte o laboratório 00 para obter instruções.

**Observação 2:** este laboratório é intitulado Opcional.  Leva pelo menos uma hora para ser concluído e exige que você seja detalhista nas etapas do laboratório.  Fique à vontade para usar o computador quando o tempo permitir.  Se a sua empresa já definiu a configuração híbrida ou não planeja usar o Azure AD Connect, pule este laboratório.

## Cenário do laboratório

Sua empresa tem um domínio local do Active Directory Domain Services.  Eles desejam manter o Active Directory local como solução de gerenciamento de identidades e acesso, mas também precisam que os usuários possam acessar os aplicativos de nuvem usando o mesmo nome de usuário e senha.

#### Tempo previsto: 60 minutos

### Exercício 1 - Configurar a infraestrutura local

#### Tarefa 1 - Criar a infraestrutura local do Active Directory

1. O modelo de implantação pode ser acessado neste link: [Guia do laboratório de teste local.](https://github.com/maxskunkworks/TLG/tree/master/tlg-base-config_3-vm)

    **Observação para alunos e MCTs** - A implantação desse modelo pode levar de 30 a 60 minutos; portanto, prepare-se para fazer uma pausa nesta etapa ou execute a implantação antes da seção de aula do curso.

    **Observação para provedores de laboratório** - Se possível, seria útil que os alunos concluíssem e implantassem isso como parte da configuração do ambiente de laboratório.

2. Na página **TLG (Guia do laboratório de teste) - Configuração Base de 3 VMs (v1.0),** selecione **Implantar no Azure**.

   **Observação** - A Configuração Base de 3 VMs provisiona um controlador de domínio do Active Directory do Windows Server 2016 chamado DC1 usando o nome de domínio especificado e um servidor membro do domínio chamado APP1 que executa o Windows Server 2016. Ele também oferece uma opção para provisionar uma VM cliente que executa o Windows 10; no entanto, não a usaremos em nosso laboratório (principalmente devido aos requisitos de licenciamento aplicáveis ao executar VMs do Windows 10 no Azure). O servidor membro do domínio (APP1) instalou automaticamente o .NET 4.5 e o IIS.  
   
   **Observação** - A VM necessária para este laboratório é **DC1**.  Se você estiver usando um Azure Pass, há uma limitação de 2 VMs; portanto, a VM do cliente pode falhar.  Isso não é necessário para este laboratório.

3. Na página **Implantação personalizada**, especifique as configurações a seguir e selecione **Examinar + Criar** e **Criar**.

   -   Assinatura: o nome da assinatura do Azure de destino na qual você deseja provisionar as VMs do Azure do ambiente de laboratório.
   -   Grupo de recursos: (Criar novo) **hybrididentity-RG**
   -   Local: o nome da região do Azure que hospedará as VMs do Azure do ambiente de laboratório.
   -   Nome da configuração: **TlgBaseConfig-01**
   -   Nome de domínio: **corp.contoso.com**.com
   -   Sistema operacional: **2016-Datacenter**
   -   Nome de usuário do administrador: **demouser**
   -   Senha do administrador: **insira uma senha segura que você vai lembrar**
   -   Implantar VM de cliente: **Não**
   -   URI de VHD do cliente: **deixe em branco**
   -   Tamanho da VM: **Standard_D2s_v3**
   
   **Observação** - Use um tamanho de VM semelhante se sua assinatura não oferecer suporte ao tamanho listado. Confira a documentação no link: <https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sizes>.

   -   Prefixo do rótulo DNS: **qualquer nome DNS válido e globalmente exclusivo (uma cadeia de caracteres exclusiva que consiste em letras, dígitos e hifens, começando com uma letra e até 47 caracteres).**

   -   Local de _artifacts: **aceitar os padrões**
   -   Token Sas do local de _artifacts: **deixe em branco**

4. Selecione **Examinar + criar**.

5. Quando a validação for aprovada, selecione **Criar**.
    
6. Aguarde até que a implantação seja concluída. Isso pode levar cerca de 60 minutos.


### Tarefa 2 - Configurar o ambiente de laboratório das VMs do Azure

1. Na janela do navegador que exibe o portal do Azure, navegue até a VM do Azure **DC1** e conecte-se a ela por meio da Área de Trabalho Remota. Quando solicitado, entre usando as seguintes credenciais:

   -   Nome de usuário: **demouser**
   -   Senha: **use a senha segura criada na Tarefa 1**

2.  Na sessão de Área de Trabalho Remota com **DC1**, inicie o **Windows PowerShell ISE**, adicione o seguinte script ao painel de scripts e execute-o para desabilitar a configuração de segurança aprimorada do Internet Explorer e o Controle de Acesso do Usuário nas VMs do Azure **DC1** e **APP1**:

    ```pwsh

    $vmNames = @('dc1','app1')
    Invoke-Command -ComputerName $vmNames {Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0}
    Invoke-Command -ComputerName $vmNames {Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A8-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0}
    Invoke-Command -ComputerName $vmNames {Set-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "ConsentPromptBehaviorAdmin" -Value 00000000}
    ```

    **Observação:** para executar vários scripts do PowerShell no mesmo arquivo, você pode realçar um script específico e selecionar **Executar Seleção** ao lado do botão verde de reprodução. 

3.  Na janela do **Windows PowerShell ISE**, adicione o seguinte script ao painel de scripts e execute-o para instalar as Ferramentas de Administração de Servidor Remoto nas VMs do Azure **DC1* e **APP1**:

    ```pwsh

    $vmNames = @('dc1','app1')
    Invoke-Command -ComputerName $vmNames {Install-WindowsFeature RSAT -IncludeAllSubFeature} 
    ```

4.  Na janela do **Windows PowerShell ISE**, adicione o seguinte script ao painel de scripts e execute-o para habilitar o TLS 1.2 nas VMs do Azure **DC1* e **APP1**:

    ```pwsh

    $vmNames = @('dc1','app1')
    Invoke-Command -ComputerName $vmNames {New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Force}
    Invoke-Command -ComputerName $vmNames {New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Force}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'Enabled' -value 1 –PropertyType DWORD}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'DisabledByDefault' -value 0 –PropertyType DWORD}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'Enabled' -value 1 –PropertyType DWORD}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'DisabledByDefault' -value 0 –PropertyType DWORD}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -name 'SchUseStrongCrypto' -value 1 –PropertyType DWORD}
    ```

5.  Na janela do **Windows PowerShell ISE**, adicione o seguinte script ao painel de scripts e execute-o para configurar a Autenticação Integrada do Windows no Site Padrão hospedado na VM do Azure **APP1**:

    ```pwsh

    $vmNames = @('app1')
    Invoke-Command -ComputerName $vmNames {Enable-WindowsOptionalFeature -Online -FeatureName IIS-WindowsAuthentication}
    Invoke-Command -ComputerName $vmNames {Set-WebConfigurationProperty -Filter "/system.webServer/security/authentication/anonymousAuthentication" -Name Enabled -Value False -PSPath IIS:\ -Location "Default Web Site"}
    Invoke-Command -ComputerName $vmNames {Set-WebConfigurationProperty -Filter "/system.webServer/security/authentication/windowsAuthentication" -Name Enabled -Value True -PSPath IIS:\ -Location "Default Web Site"}
    ```

### Tarefa 3 - Reiniciar as VMs do Azure

1. Na janela do **Windows PowerShell ISE**, no painel do console, execute o seguinte para reiniciar o **APP1**:

    ```pwsh

    Restart-Computer -ComputerName 'APP1'
    ```

2. Na janela do **Windows PowerShell ISE**, no painel do console, execute o seguinte para reiniciar o **DC1**:

    ```pwsh
    Restart-Computer -ComputerName 'DC1'
    ```

### Tarefa 5 - Configurar o Active Directory contoso.local

1. Conecte-se novamente à VM do Azure **DC1** por meio da Área de Trabalho Remota. Quando solicitado, entre usando as seguintes credenciais:

    -   Nome de usuário: **demouser**

    -   Senha: **demo\@pass123**
       - **É altamente recomendado inserir uma senha segura que você possa lembrar.**

2.  Na sessão de Área de Trabalho Remota com **DC1**, inicie o Internet Explorer e acesse o link abaixo.

    ```
    https://github.com/microsoft/MCW-Hybrid-identity/tree/main/Hands-on%20lab/studentfiles
    ```

3. Na página **Criar Usuários/Grupo para Demonstração do Active Directory/Teste de Ambiente**, clique no link **CreateDemoUsers.ps1**, aceite os termos de licenciamento e salve o script correspondente no sistema de arquivos local.

4. Na página **Criar Usuários/Grupo para Demonstração do Active Directory/Teste de Ambiente**, clique no link **CreateDemoUsers.csv** (diretamente acima da seção de código do PowerShell) e salve o arquivo csv correspondente no mesmo local que o arquivo **CreateDemoUsers.ps1**.

5. Na sessão de Área de Trabalho Remota com **DC1**, inicie o Explorador de Arquivos, procure a pasta onde você baixou os arquivos, clique com o botão direito do mouse no arquivo **CreateDemoUsers.ps1**, selecione **Propriedades**, na caixa de diálogo **Propriedades de CreateDemoUsers.ps1**, marque a caixa de seleção **Desbloquear** e selecione **OK**.

6. Na janela do Explorador de Arquivos, clique novamente com o botão direito do mouse no arquivo **CreateDemoUsers.ps1** e selecione **Editar**. 

7. Na janela **Administrador: Windows PowerShell ISE**, altere a linha **148** de:

    ```pwsh
    $UserCount = 1000 #Up to 2500 can be created
    ```

   para
    ```pwsh
    $UserCount = 2500 #Up to 2500 can be created
    ```

8. Na janela **Windows PowerShell ISE**, salve a alteração e execute o script**CreateDemoUsers.ps1** para criar uma hierarquia de unidade organizacional de ambiente de laboratório e preencha com contas de usuário de teste. 

9.  Na janela do **Windows PowerShell ISE**, adicione o seguinte script ao painel de scripts e execute-o para modificar as configurações das contas de usuário do AD que você usará neste laboratório:

    ```pwsh

    $adUser1 = Get-ADUser -Filter {samAccountName -eq "AGAyers"}
    $adUser1groups = $adUser1 | Get-ADPrincipalGroupMembership 
    $adUser1groups | foreach { if ($_.name -ne 'Domain Users') {Remove-ADPrincipalGroupMembership -MemberOf $_.name -Identity $adUser1.DistinguishedName} }
    Add-ADPrincipalGroupMembership -MemberOf 'Engineering' -Identity $adUser1.DistinguishedName
    Move-ADObject -Identity $adUser1.DistinguishedName -TargetPath 'OU=NJ,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'

    Set-ADAccountPassword -Identity 'CN=Ayers\, Ann,OU=NJ,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com' -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "demo@pass123" -Force)

    $adUser2 = Get-ADUser -Filter {samAccountName -eq "TFBell"}
    $adUser2groups = $adUser2 | Get-ADPrincipalGroupMembership 
    $adUser2groups | foreach { if ($_.name -ne 'Domain Users') {Remove-ADPrincipalGroupMembership -MemberOf $_.name -Identity $adUser2.DistinguishedName} }
    Add-ADPrincipalGroupMembership -MemberOf 'Engineering' -Identity $adUser2.DistinguishedName
    Move-ADObject -Identity $adUser2.DistinguishedName -TargetPath 'OU=VT,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'

    Set-ADAccountPassword -Identity 'CN=Bell\, Teresa,OU=VT,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com' -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "demo@pass123" -Force)
    Get-ADGroup -Identity 'Domain Admins' | Add-ADGroupMember -Members 'CN=Ayers\, Ann,OU=NJ,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'
    Get-ADGroup -Identity 'Enterprise Admins' | Add-ADGroupMember -Members 'CN=Ayers\, Ann,OU=NJ,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'
    ```

10. Na janela do **Windows PowerShell ISE**, adicione o seguinte script ao painel de scripts e execute-o para criar unidades organizacionais adicionais chamadas **Servidores** e **Clientes** e mova a conta de computador **APP1** para a primeira delas:

    ```pwsh

    New-ADOrganizationalUnit -Name 'Servers' -Path 'OU=Demo Accounts,DC=corp,DC=contoso,DC=com'
    New-ADOrganizationalUnit -Name 'Clients' -Path 'OU=Demo Accounts,DC=corp,DC=contoso,DC=com'

    Move-ADObject -Identity 'CN=APP1,CN=Computers,DC=corp,DC=contoso,DC=com' -TargetPath 'OU=Servers,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'
    ```

11. Saia do **DC1**.

## Exercício 2: Integrar uma floresta do Active Directory a um locatário do Azure Active Directory

### Tarefa 1: Criar um locatário do Azure Active Directory e ativar uma avaliação do EMS E5

Nesta tarefa, você criará um locatário do Azure Active Directory com as seguintes configurações: 

-   Nome da organização: **Contoso**

-   Nome de domínio inicial: qualquer nome de domínio válido e exclusivo.

-   País ou região: **Estados Unidos**

1. No computador do laboratório, inicie uma nova janela do navegador da web e acesse o portal do Azure em <https://portal.azure.com>, se ainda não tiver feito isso.

2. Quando solicitado, entre na assinatura do Azure na qual você implantou os recursos nos exercícios Antes do Laboratório Prático.

3. No computador do laboratório, no portal do Azure, selecione **+ Criar um recurso**.

4. Na página **Novo**, na caixa de texto **Pesquisar no Marketplace**, digite **Azure Active Directory** e, lista de resultados, selecione **Azure Active Directory**.

5. Na página do **Azure Active Directory**, selecione **Criar**.

6. Na página **Criar diretório**, especifique as seguintes configurações e selecione **Criar**:

Guia Básico:
    -   Selecionar um tipo de locatário: escolha **Azure Active Directory**

Guia Configuração:
    -   Nome da organização: **Contoso**

    -   Nome de domínio inicial: qualquer nome de domínio válido e exclusivo.

    -   País ou região: **Estados Unidos**

7. Depois de criado, abra o **Azure Active Directory**.

8. Na página Visão geral, selecione **Gerenciar locatários**.

9. Faça uma verificação em seu diretório recém-criado.

10. Na parte superior da página, escolha **Alternar**.

    >**Observação**: pode demorar alguns minutos para tudo ser exibido corretamente.

11. Na página **Contoso - Visão geral**, selecione **Usuários**.

12. Observe que você só tem um único usuário do ExternalAzureAD nesse novo locatário.

### Tarefa 2: criar e configurar o usuário do Azure AD para administrar esse diretório

1. No computador do laboratório, no portal do Azure, retorne à página **Contoso - Visão geral**.

2. Na página **Contoso - Visão geral**, selecione **Usuários** em **Gerenciar** na navegação esquerda.

3. Na página **Usuários - Todos os usuários**, selecione a entrada que representa sua conta de usuário.

4. Na página **Perfil** da conta de usuário, selecione **Editar**.

5. Na seção **Configurações**, na lista suspensa **Local de uso**, selecione a entrada **Estados Unidos** e clique em **Salvar**.

#### Criar o novo administrador

6. Na página **Novo usuário**, verifique se a opção **Criar usuário** está selecionada, especifique as seguintes configurações e clique em **Criar**:

    - Nome de usuário: **john.doe *@your seu nome de domínio de locatário do Azure AD* ** onde ***seu nome de domínio do locatário do Azure AD*** é o nome de domínio especificado ao criar o locatário do Azure AD da Contoso.

    - Nome: **john.doe**

    - Nome: **John**

    - Sobrenome: **Doe**
    
    - Senha: **gerar a senha automaticamente**
    
    - Mostrar senha: **habilitado** e certifique-se de copiar a senha.

    - Grupos: **0 grupo selecionado**
    
    - Funções: **Administrador Global**
    
    - Bloquear entrada: **Não**
    
    - Local de Uso: **Estados Unidos**
    
    - Cargo: **Deixar em branco**
    
    - Departamento: **Deixar em branco**

    > **Observação**: copie os valores de **Nome de usuário** e **Senha** para o bloco de notas. Você precisará deles mais adiante neste laboratório.


### Tarefa 5: Configurar o sufixo DNS na floresta do Active Directory da Contoso

Nesta tarefa, você configurará o sufixo DNS da floresta do Active Directory da Contoso para corresponder ao nome de domínio personalizado do Azure AD recém-verificado.

1. No computador do laboratório, no portal do Azure, verifique se você está conectado ao locatário do Azure AD associado à assinatura do Azure na qual você implantou os recursos nos exercícios Antes do Laboratório Prático (o **Diretório Padrão**). Caso contrário, clique no ícone **Diretório + Assinatura** na barra de ferramentas do portal do Azure (à direita do ícone do **Cloud Shell**) para alternar para esse locatário do Azure AD. 

2. No portal do Azure, navegue até a página da máquina virtual **DC1**.

3. Na página da máquina virtual **DC1**, conecte-se à **DC1** por meio da Área de Trabalho Remota. Quando solicitado a fazer logon, use o nome **demouser** e a senha **demo\@pass123**. 

4. Na sessão de Área de Trabalho Remota com **DC1**, na janela **Gerenciador de Servidores**, inicie o console **Domínios e Objetos de Confiança do Active Directory** nas **Ferramentas**. 

5. No console **Domínios e Objetos de Confiança do Active Directory** clique com o botão direito em **Domínios e Objetos de Confiança do Active Directory [DC1.corp.contoso.com]** à esquerda e selecione **Propriedades**.

6. Na guia **Sufixos UPN** da janela **Domínios e Objetos de Confiança do Active Directory [DC1.corp.contoso.com]**, na caixa de texto **Sufixos UPN alternativos**, digite o nome do domínio personalizado verificado na tarefa anterior, selecione **Adicionar** e clique em **OK**.

7. Na sessão de Área de Trabalho Remota com **DC1**, na janela **Gerenciador de Servidores**, inicie o console **Usuários e Computadores do Active Directory** em **Ferramentas**. 

8. No console **Usuários e Computadores do Active Directory**, expanda **corp.contoso.com** à esquerda e examine a hierarquia de unidade organizacional do domínio e a associação de grupo dos grupos de domínio. 

9.  Na sessão de Área de Trabalho Remota com **DC1**, inicie o Windows PowerShell ISE e, no painel Script, execute o seguinte para substituir o sufixo UPN de todos os usuários que são membros do grupo **Engenharia** pelo que corresponde ao nome de domínio personalizado verificado do locatário do Azure AD da Contoso (substitua o espaço reservado `<custom_domain_name>` pelo nome real do nome de domínio personalizado verificado atribuído ao locatário do Azure AD da Contoso). 

    ```pwsh
    $domainName = '<custom_domain_name>'
    $users = Get-ADGroupMember -Identity 'Engineering' -Recursive | Where-Object {$_.objectClass -eq 'user'}

    foreach ($user in $users) {
        $user = Get-ADUser -Identity $User.SamAccountName
        $userName = $user.UserPrincipalName.Split('@')[0] 
        $upn = $userName + "@" + $domainName 
        $user | Set-ADUser -UserPrincipalName $upn
    }
    ```

### Tarefa 6: Instalar o Azure AD Connect

Nesta tarefa, você instalará o Azure AD Connect.

1. Na sessão de Área de Trabalho Remota com **DC1**, no Gerenciador de Servidores, selecione **Servidor Local** e verifique se **Configuração de Segurança Reforçada do IE** está desabilitada. Caso contrário, clique no link **Ativado** ao lado de **Configuração de Segurança Reforçada do IE**, defina as configurações de **Administradores** como **Desativado** e clique em**OK**.

2. Na sessão da Área de Trabalho Remota com **DC1**, abra a janela do **Windows PowerShell ISE** e execute este comando para instalar o navegador Chrome.

    ```pwsh
    $LocalTempDir = $env:TEMP; $ChromeInstaller = "ChromeInstaller.exe"; (new-object System.Net.WebClient).DownloadFile('http://dl.google.com/chrome/install/375.126/chrome_installer.exe', "$LocalTempDir\$ChromeInstaller"); & "$LocalTempDir\$ChromeInstaller" /silent /install; $Process2Monitor = "ChromeInstaller"; Do { $ProcessesFound = Get-Process | ?{$Process2Monitor -contains $_.Name} | Select-Object -ExpandProperty Name; If ($ProcessesFound) { "Still running: $($ProcessesFound -join ', ')" | Write-Host; Start-Sleep -Seconds 2 } else { rm "$LocalTempDir\$ChromeInstaller" -ErrorAction SilentlyContinue -Verbose } } Until (!$ProcessesFound)
    ```

2. Na sessão de Área de Trabalho Remota com **DC1**, inicie o navegador Chrome e acesse o portal do Azure em <https://portal.azure.com>.

3. Quando solicitado a entrar, insira as credenciais da conta de usuário do Azure AD de **john.doe** que você copiou no Bloco de Notas anteriormente neste exercício.

4. Quando solicitado, altere a senha para a conta de usuário **john.doe**. 
  
    > **Observação**: se você receber a mensagem **Já vimos essa senha muitas vezes antes. Escolha algo mais difícil de adivinhar**, precisará modificar a senha até que ela seja única o suficiente para ser aceita.

5. Se você receber a mensagem **Continuar conectado?"**, selecione **Não**. Você será redirecionado para a interface do portal do Azure. 

6. Se for apresentada a caixa de diálogo **Bem-vindo ao Microsoft Azure**, selecione **Talvez mais tarde**. 

7. No portal do Azure, selecione **Azure Active Directory** na navegação esquerda do portal para acessar a página **Contoso - Visão geral**.

8. Na página **Contoso - Visão Geral**, selecione **Azure AD Connect** em **Gerenciar** à esquerda.

9.  Na página **Azure AD Connect**, clique no link **Baixar Azure AD Connect**.  Em seguida, escolha **Conectar sincronização** no menu.

10. Na página da Web **Microsoft Azure Active Directory Connect** do site de Downloads da Microsoft, selecione **Baixar**.

11. Quando solicitado a executar ou salvar o **AzureADConnect.msi**, selecione **Executar**. O arquivo será baixado e o assistente do **Microsoft Azure Active Directory Connect** será iniciado automaticamente. 

12. Na página **Bem-vindo ao Azure AD Connect**, marque a caixa **Eu concordo com os termos de licença e o aviso de privacidade** e clique em **Continuar**.

13. Na página **Configurações expressas**, clique no botão **Personalizar**.

14. Na página **Instalar componentes requeridos**, deixe todas as opções de configuração opcionais desmarcadas e clique em **Instalar**.

15. Na página **Entrada do usuário**, clique no botão **Autenticação de passagem**, selecione **Habilitar logon único** e, em seguida, selecione **Avançar**.

16. Na página **Conectar ao Azure AD**, entre usando as credenciais da conta **john.doe** e selecione **Avançar**.

17. Na página **Conectar seus diretórios**, verifique se a entrada **corp.contoso.com** aparece na lista suspensa **FLORESTA** e selecione **Adicionar Diretório**. Na **Conta da floresta do AD**, verifique se a opção **Criar nova conta do AD** está selecionada; na caixa de texto **NOME DE USUÁRIO DE ADMINISTRADOR CORPORATIVO**, digite **CORP.CONTOSO.COM\\demouser**; na caixa de texto **SENHA**, digite **demo\@pass123** e selecione **OK**.


18. Ainda na página **Conectar seus diretórios**, selecione **Avançar**.

19. Na página **Configuração de entrada do Azure AD**, verifique se seu nome de domínio personalizado está listado como **Sufixo UPN do Active Directory** verificado e que a **userPrincipalName** aparece na lista suspensa **NOME PRINCIPAL DO USUÁRIO** Observe o aviso informando que os **usuários não poderão entrar no Azure AD com credenciais locais se o sufixo UPN não corresponder a um nome de domínio verificado**. Marque a caixa **Continuar sem correspondência com todos os sufixos UPN para domínios verificados** e selecione **Avançar**. 

    >**Observação**: isso é esperado, já que alguns usuários ainda estão configurados com o sufixo UPN **contoso.local**, que não é roteável e não pode ser configurado como um nome de domínio personalizado verificado de um locatário do Azure AD.

20. Na página **Domínio e filtragem UO**, escolha **Sincronizar domínios e UOs selecionados** e, em seguida, certifique-se de que apenas a UO **DemoAccounts** e todas as UOs filhas estejam selecionadas e selecione **Avançar**. 


21. Na página **Identificar exclusivamente seus usuários**, aceite as configurações padrão e selecione **Avançar**. 


22. Na página **Filtrar usuários e dispositivos**, aceite as configurações padrão e selecione **Avançar**. 

23. Na página **Recursos Opcionais**, aceite as configurações padrão e selecione **Avançar**.

24. Na página **Habilitar logon único**, selecione **Inserir credenciais**; na caixa de diálogo **Credenciais da Floresta**, entre com o nome de usuário **CORP\\demouser** e a senha **demo\@pass123** e selecione **Avançar**.


25. Na página **Pronto para configurar**, verifique se a caixa de seleção**Inicie o processo de sincronização quando a configuração for concluída** **NÃO** está marcada e selecione **Instalar**.


   > **Observação**: você configurará a filtragem em nível de atributo antes de habilitar o processo de sincronização.

   > **Observação**: a instalação deve levar cerca de dois minutos.

26. Na página **Configuração completa**, selecione **Sair**.


### Tarefa 7: Habilitar a lixeira do Active Directory

Nesta tarefa, você habilitará a Lixeira no domínio do Active Directory da Contoso. 

1. Na sessão de Área de Trabalho Remota com **DC1**, no menu Ferramentas no console do Gerenciador de Servidores, inicie o **Centro Administrativo do Active Directory**.


2. No console do **Centro Administrativo do Active Directory**, selecione **corp (local)** à esquerda e selecione **Habilitar Lixeira** Quando sua confirmação for solicitada, selecione **OK**.


3. Quando solicitado a atualizar o Centro Administrativo do AD, selecione **OK.**

   > **Observação**: para obter informações sobre os benefícios da Lixeira em cenários híbridos, confira<https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-sync-recycle-bin>

### Tarefa 8: Configurar a filtragem em nível de atributo do Azure AD Connect

Nesta tarefa, você configurará a filtragem em nível de atributo do Azure AD Connect que limitará a sincronização de contas de usuário àquelas com o sufixo UPN correspondente ao nome de domínio personalizado do locatário do Azure AD de destino.

   > **Observação**: a opção de filtragem positiva requer pelo menos duas regras de sincronização. Um deles determina o escopo correto dos objetos a serem sincronizados. A segunda regra de sincronização pega-tudo filtra todos os objetos ainda não identificados como um objeto a ser sincronizado.

1. Na sessão de Área de Trabalho Remota com **DC1**, inicie o **Editor de Regras de Sincronização** no **Azure AD Connect** no menu Iniciar.


2. Na janela Editor de regras de sincronização, na página **Exibir e gerenciar suas regras de sincronização**, verifique se **Entrada** aparece na lista suspensa **Direção** e selecione **Adicionar nova regra**. O assistente **Criar regra de sincronização de entrada** será iniciado.


3. Na página **Criar regra de sincronização de entrada - Descrição**, especifique as seguintes configurações e selecione **Avançar**:

    - Nome: **Entrada personalizada do AD - Filtro UPN**

    - Descrição: **Regra de entrada personalizada - inclui usuários com UPN definido para corresponder ao domínio personalizado do Azure AD**

    - Sistema conectado: **corp.contoso.com**

    - Tipo de objeto do sistema conectado: **usuário**

    - Tipo de objeto do Metaverso: **pessoa**

    - Tipo de link: **junção**

    - Precedência: **50**

    - Marcação: **deixar em branco**

    - Habilitar sincronização de senha: **deixar em branco**

    - Desabilitado: **deixar em branco**


4. Na página **Criar filtro de escopo de entrada**, selecione **Adicionar grupo**, selecione **Adicionar cláusula**, especifique o seguinte e selecione **Avançar**:

    - Atributo: **userPrincipalName**

    - Operador: **ENDSWITH**

    - Valor: **\@\<your custom domain name>**

5. Na página **Regras de ingresso**, selecione **Avançar**.

6. Na página **Transformações**, selecione **Adicionar transformação**, especifique o seguinte e selecione **Adicionar**:

    - FlowType: **Constante**

    - Atributo de Destino: **cloudFiltered**

    - Fonte: **Falso**

7. Quando for apresentada a caixa de diálogo de **Aviso** com a mensagem **Uma importação e sincronização completas serão executadas em 'corp.contoso.com' durante o próximo ciclo de sincronização**, selecione **OK.**

   > **Observação**: isso deve levá-lo de volta à interface Exibir e gerenciar suas regras de sincronização, com a nova regra listada na parte superior da lista de regras. 

8. Ainda na janela **Editor de Regras de Sincronização**, na página **Exibir e gerenciar suas regras de sincronização**, verifique se **Entrada** aparece na lista suspensa **Direção** e selecione novamente **Adicionar nova regra**. O assistente **Criar regra de sincronização de entrada** será iniciado.

9. Na página **Descrição**, especifique as seguintes configurações e selecione **Avançar**:

    - Nome: **Entrada personalizada do AD - Filtro pega-tudo**

    - Descrição: **Regra de Entrada Personalizada - exclui todos os usuários com UPN não definido para corresponder ao domínio personalizado do Azure AD**

    - Sistema conectado: **corp.contoso.com**

    - Tipo de objeto do sistema conectado: **usuário**

    - Tipo de objeto do Metaverso: **pessoa**

    - Tipo de link: **junção**

    - Precedência: **51**

    - Marcação: **deixar em branco**

    - Habilitar sincronização de senha: **deixar em branco**

    - Desabilitado: **deixar em branco**


10. Na página **Filtro de Escopo**, clique em **Avançar**.

11. Na página **Regras de ingresso**, selecione **Avançar**.

12. Na página **Transformações**, selecione **Adicionar transformação**, especifique o seguinte e selecione **Adicionar**:

    - FlowType: **Constante**

    - Atributo de Destino: **cloudFiltered**

    - Fonte: **Verdadeiro**

13. Quando for apresentada a caixa de diálogo de **Aviso** com a mensagem **Uma importação e sincronização completas serão executadas em 'corp.contoso.com' durante o próximo ciclo de sincronização**, selecione **OK.**

    >**Observação**: isso deve levá-lo de volta à interface **Exibir e gerenciar suas regras de sincronização**, com as novas regras listadas na parte superior da lista de regras. 

### Tarefa 9: Iniciar e verificar a sincronização de diretório

1. Na sessão de Área de Trabalho Remota com **DC1**, clique duas vezes no atalho da área de trabalho do **Azure AD Connect**.

2. Na página **Bem-vindo ao Azure AD Connect**, clique em **Configurar**. 

3. Na página **Tarefas adicionais**, selecione **Personalizar opções de sincronização** e selecione **Avançar**.

4. Na página **Conectar ao Azure AD**, entre usando as credenciais da conta **john.doe** e selecione **Avançar**.

5. Na página **Conectar seus diretórios**, selecione **Avançar**.

6. Na página **Filtragem de domínio e UO**, selecione **Avançar**. 

7. Na página **Recursos opcionais**, aceite as configurações padrão e selecione **Avançar**.

8. Na página **Habilitar logon único**, selecione **Avançar**.

9. Na página **Pronto para configurar**, marque a caixa de seleção **Iniciar o processo de sincronização quando a configuração for concluída** e selecione **Configurar**.

10. Na página **Configuração completa**, selecione **Sair**.

11. Na sessão de Área de Trabalho Remota com **DC1**, na janela do navegador Edge que exibe o portal do Azure, acesse a página **Usuários - Todos os usuários** do locatário do Azure AD da Contoso.

12. Na página **Usuários - Todos os usuários**, observe que a lista de objetos de usuário inclui todas as contas de usuário com o sufixo UPN correspondente ao nome de domínio personalizado do locatário do Azure AD. Talvez seja necessário atualizar a página ou aguardar alguns minutos para ver a alteração.

13. No portal do Azure, acesse a página **Grupos - Todos os grupos** do locatário do Azure AD da Contoso e observe que todos os grupos de domínio de corp.contoso.com também foram sincronizados. 

14. No portal do Azure, acesse a página **Contoso - Azure AD Connect** e selecione **Azure AD Connect** à esquerda. Verifique se as seguintes configurações foram definidas: 

    - Status de sincronização do Azure AD Connect: **Habilitado** 
  
    - Última sincronização: **Este deve ser algum tipo de carimbo de data/hora**. 
  
    - Sincronização de hash de senha: **desabilitada** 
  
    - Federação: **desabilitada**
   
    - Logon único contínuo: **habilitado para 1 domínio** 
  
    - Autenticação de passagem: **habilitado com 1 agente**

   > **Observação**: em um ambiente de produção, você instalaria agentes adicionais para redundância. Para obter mais informações, consulte <https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-pta-quick-start>.

### Tarefa 10: Configurar ingresso no Azure AD híbrido

Nesta tarefa, você configurará as opções de sincronização de dispositivo do Azure AD Connect.

1. Na sessão de Área de Trabalho Remota com **DC1**, clique duas vezes no atalho da área de trabalho do **Azure AD Connect**.

2. Na página **Bem-vindo ao Azure AD Connect**, clique em **Configurar**. 

3. Na página **Tarefas adicionais**, selecione **Configurar opções do dispositivo** e selecione **Avançar**.

4. Na página **Visão geral**, revise as informações sobre **Ingresso no Azure AD híbrido** e **Write-back de dispositivo** e selecione **Avançar**.

5. Na página **Conectar ao Azure AD**, entre usando as credenciais da conta **john.doe** e selecione **Avançar**.

6. Na página **Opções do dispositivo**, selecione **Configurar ingresso no Azure AD híbrido** e, em seguida, selecione **Avançar**. 

7. Na página **Sistema operacional do dispositivo**, marque as caixas de seleção **Dispositivos associados ao domínio do Windows 10 ou versões posteriores** e **Dispositivos com suporte ingressados no domínio de nível inferior do Windows** e selecione **Avançar**. 

   > **Observação**: os dispositivos de nível inferior do Windows são suportados somente se você estiver usando SSO contínuo para domínios gerenciados ou um serviço de federação, como o AD FS para domínios federados.

8. Na página **Configuração do SCP**, marque a caixa da floresta do Active Directory **corp.contoso.com**, selecione a entrada **Azure Active Directory** na lista suspensa **Serviço de Autenticação** e clique em **Adicionar**.

9. Quando solicitado a fornecer as Credenciais de Administrador Corporativo de corp.contoso.com, na caixa de diálogo **Segurança do Windows**, entre com o nome de usuário **CORP\\demouser** e a senha **demo\@pass123**.

10. Ainda na página **Configuração do SCP**, selecione **Avançar**.

11. Na página **Pronto para configurar**, selecione **Configurar**.

12. Na página **Configuração concluída**, verifique se a tarefa foi concluída com sucesso e selecione **Sair**.


### Tarefa 11: Realizar ingresso no Azure AD híbrido

1. No computador do laboratório, no portal do Azure, verifique se você está conectado ao locatário do Azure AD associado à assinatura do Azure na qual você implantou os recursos nos exercícios Antes do Laboratório Prático (o **Diretório Padrão**). Caso contrário, clique no ícone **Diretório + Assinatura** na barra de ferramentas do portal do Azure (à direita do ícone do **Cloud Shell**) para alternar para esse locatário do Azure AD. 

2. No portal do Azure, acesse a página da máquina virtual **APP1**.

3. Na página da máquina virtual **APP1**, conecte-se ao **APP1** por meio da Área de Trabalho Remota. Quando solicitado a entrar, use o nome de usuário **AGAyers\@<custom_domain_name>** com a senha **demo@pass123** (onde o espaço reservado **<custom_domain_name>** representa o nome de domínio DNS personalizado que você atribuiu ao locatário do Azure AD da Contoso anteriormente neste exercício.

4. Na sessão de Área de Trabalho Remota com **APP1**, na janela **Gerenciador de Servidores**, inicie o **Agendador de Tarefas** nas **Ferramentas**. 


5. No console **Agendador de Tarefas**, expanda **Biblioteca do Agendador de Tarefas** > **Microsoft** > **Windows** > **Workplace Join**. Habilite e execute a tarefa **Automatic-Device-Join**. 


6. Alterne para a sessão de Área de Trabalho Remota com **DC1** e, no painel de console da janela do Windows PowerShell ISE, inicie a sincronização delta do Azure AD Connect executando o seguinte:

   ```pwsh
   Import-Module -Name 'C:\Program Files\Microsoft Azure AD Sync\Bin\ADSync\ADSync.psd1'
   
   Start-ADSyncSyncCycle -PolicyType Delta
   ```

7. Retorne à sessão de Área de Trabalho Remota com **APP1** e inicie um **Prompt de Comando**.

8. Na janela do Prompt de Comando, verifique o status de registro do Azure AD do APP1 executando o seguinte: 

   ```
   dsregcmd /status
   ```

9. Verifique se a saída do comando é semelhante ao seguinte:

   ```
   +----------------------------------------------------------------------+
   | Device State                                                         |
   +----------------------------------------------------------------------+

        AzureAdJoined : YES
     EnterpriseJoined : NO
             DeviceId : 61eea2b8-efbe-43d9-b267-126433c8ee34
           Thumbprint : BBAAA0FB4A55E880388851BED955A2669A961A96
       KeyContainerId : 2eb75eb8-0a1d-437b-99d9-9dd161ca0d90
          KeyProvider : Microsoft Software Key Storage Provider
         TpmProtected : NO
         KeySignTest: : PASSED
                  Idp : login.windows.net
             TenantId : xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx
           TenantName : xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx
          AuthCodeUrl : https://login.microsoftonline.com/xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx/oauth2/authorize
       AccessTokenUrl : https://login.microsoftonline.com/xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx/oauth2/token
               MdmUrl :
            MdmTouUrl :
     MdmComplianceUrl :
          SettingsUrl :
       JoinSrvVersion : 1.0
           JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/
            JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net
        KeySrvVersion : 1.0
            KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/
             KeySrvId : urn:ms-drs:enterpriseregistration.windows.net
         DomainJoined : YES
           DomainName : CORP

   +----------------------------------------------------------------------+
   | User State                                                           |
   +----------------------------------------------------------------------+

               NgcSet : NO
      WorkplaceJoined : NO
        WamDefaultSet : NO
           AzureAdPrt : NO

   +----------------------------------------------------------------------+
   | Ngc Prerequisite Check                                               |
   +----------------------------------------------------------------------+

        IsUserAzureAD : NO
        PolicyEnabled : NO
       DeviceEligible : YES
   SessionIsNotRemote : NO
     X509CertRequired : NO
         PreReqResult : WillNotProvision

   ```
11. Retorne à sessão de Área de Trabalho Remota com **DC1**; na janela do navegador Edge que exibe o portal do Azure, acesse a página **Dispositivos - Todos os dispositivos** do locatário do Azure AD da Contoso e verifique se há uma entrada representando o servidor APP1, com **Tipo de ingresso** definido como **Ingressado no Azure AD híbrido**.

   > **Observação**: talvez seja necessário aguardar até que o status de registro do Azure AD seja relatado corretamente e seu objeto do Azure AD apareça no portal do Azure.


