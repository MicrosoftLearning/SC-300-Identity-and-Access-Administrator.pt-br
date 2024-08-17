---
lab:
  title: 01 - Gerenciar funções do usuário
  learning path: '01'
  module: Module 01 - Implement an Identity Management Solution
---

# Locatários do WWL – Termos de uso
Se você estiver recebendo um locatário como parte de uma entrega de treinamento com instrutor, observe que o locatário é disponibilizado com a finalidade de dar suporte aos laboratórios práticos no treinamento com instrutor. Os locatários não devem ser compartilhados ou usados para fins fora dos laboratórios práticos. O locatário usado neste curso é um locatário de avaliação e não pode ser usado ou acessado após o fim da aula e não está qualificado para extensão. Os locatários não podem ser convertidos em uma assinatura paga. Os locatários obtidos como parte deste curso permanecem a propriedade da Microsoft Corporation e reservamos o direito de obter acesso e a qualquer momento. 



# Laboratório 01: Gerenciar funções de usuários

## Cenário do laboratório

Sua empresa contratou recentemente um novo funcionário que desempenhará funções como administrador de aplicativos. Você deve criar um novo usuário e atribuir a função apropriada.

#### Tempo previsto: 30 minutos

### Exercício 1 - Criar um novo usuário e testar seus direitos de administrador de aplicativo

#### Tarefa 1 - Adicionar um novo usuário

1. Faça logon em [https://entra.microsoft.com](https://entra.microsoft.com) como um administrador global

2. Selecione **Identidade** no menu à esquerda.

3. No menu de navegação à esquerda, em **Usuários**, selecione **Todos os Usuários** e, em seguida, **+ Novo Usuário** e **Criar novo usuário**.

4. Marque o botão **Criar usuário**. Crie um usuário com as seguintes informações:

    | **Configuração**| **Valor**|
    | :--- | :--- |
    | Nome UPN| ChrisG|
    | Nome para Exibição| Chris Green|

5. Marque a opção **Gerar senha automaticamente**.

6. Anote a senha gerada em um local de fácil acesso para a próxima tarefa.

     *Você terá que alterar a senha no primeiro login nesta conta*

7. Selecione **Examinar + criar**. Em seguida, selecione **Criar** na tela de revisão. O usuário é criado e registrado em sua organização.

#### Tarefa 2 - Fazer login e tentar criar um aplicativo

1. Inicie uma nova janela InPrivate do navegador.
2. Abra o centro de administração do Microsoft Entra [https://entra.microsoft.com](https://entra.microsoft.com) como Chris Green.

    | **Configuração**| **Valor**|
    | :--- | :--- |
    | Nome de usuário| ChrisG@`your domain name.com`|
    | Senha| Digite a senha gerada automaticamente na tarefa anterior. |

3. Atualize a senha.

    | **Configuração**| **Valor**|
    | :--- | :--- |
    | Senha atual| Use a senha gerada automaticamente|
    | Nova senha| Digite uma senha única e segura |
    | Confirmar senha| Digite a senha novamente |

4. Se você vir uma **caixa de diálogo de tour**, selecione o botão **Talvez mais tarde**.

5. Busque e selecione **Aplicativos empresariais** na caixa de diálogo de pesquisa na parte superior da tela.
7. Clique em **+ Novo aplicativo**. Observe que **+ Crie seu próprio aplicativo** não está disponível.

9. Tente selecionar em algumas das outras configurações, como **Proxy de Aplicativo**, **configurações do usuário**, entre outras, para ver ao que **Chris Green** não tem direitos.
10. Selecione o nome **ChrisG** no canto superior direito e saia.


### Exercício 2 - Atribuir a função de administrador de aplicativos e criar um aplicativo

#### Tarefa 1 – Atribuir uma função a um usuário

Usando o Microsoft Entra ID, você pode designar administradores limitados para gerenciar tarefas de identidade em funções com menos privilégios. Os administradores podem ser atribuídos para os fins de adicionar ou alterar os usuários, atribuir funções administrativas, redefinir senhas de usuário, gerenciar licenças de usuário e gerenciando nomes de domínio.

1. Se você ainda não estiver conectado como um administrador global, abra o centro de administração do Microsoft Entra e faça logon.
2. Navegue até Identidade e selecione a página Usuários.
3. Selecione **Todos os usuários** na seção Gerenciar do menu.
4. Selecione a conta **Chris Green**.
5. Escolha **Funções atribuídas** no menu Gerenciar.
6. Selecione **+ Adicionar atribuições** e marque a função `Application administrator`.
7. Selecione **Adicionar**

    ![Página Funções atribuídas – mostrando a função selecionada](./media/directory-role-select-role.png)

**Observação** – se o ambiente de laboratório já tiver ativado a P2 do Microsoft Entra ID Premium, o PIM (gerenciamento de identidade privilegiada) será habilitado e você precisará selecionar **Avançar** e atribuir uma função permanente a esse usuário.

9. Selecione o botão **Atualizar**.

**Observação – A função Administrador de aplicativos recém-atribuída aparece na página Funções atribuídas do usuário.**

#### Tarefa 2 - Verificar as permissões do aplicativo

1. Inicie uma nova janela InPrivate do navegador.
2. Abra o centro de administração do Microsoft Entra [https://entra.microsoftcom](https://entra.microsoft.com) como Chris Green.

    | **Configuração**| **Valor**|
    | :--- | :--- |
    | Nome de usuário| ChrisG@`your domain name.com`|
    | Senha| Insira o nome de usuário e a senha criados anteriormente. |

3. Se você vir a caixa de diálogo do tour **Bem-vindo ao Microsoft Azure**, clique no botão **Talvez mais tarde**.
4. Pesquise e selecione **Aplicativos empresariais** na caixa de diálogo de pesquisa na parte superior da tela.
5. Observe que **+ Novo Aplicativo** agora está disponível.
6. Selecione **+ Novo Aplicativo**
7. Veja que **"**+ Criar seu próprio aplicativo** não está esmaecido. Se você escolher um aplicativo de galeria, verá que o botão **Criar** está disponível.

   **Observação – Essa função agora tem a capacidade de adicionar aplicativos ao locatário. Vamos experimentar mais com esse recurso em laboratórios posteriores.**

7. Sair da instância Chris Green do portal e fechar o navegador.

### Exercício 3 - Remover uma atribuição de função

#### Tarefa 1 - Remover a função de administrador de aplicativos de Chris Green

Esta tarefa usará um método alternativo para remover a função atribuída; ela usará a opção **Funções e administradores** no Microsoft Entra ID.

1. Se você ainda não estiver conectado como administrador global, inicie o centro de administração do Microsoft Entra e faça logon agora.
2. Na caixa de pesquisa, digite **Funções e**, em seguida, inicie as Funções e administração do Microsoft Entra ID.
3. Em  **Todas as funções** de  **Funções e administradores**, selecione a função **Administrador de aplicativo** na lista.
4. Na página **Administrador do aplicativo | Atribuições** você deve ver o nome de Chris Green listado.
5. Marque a caixa ao lado de Chris Green.
6. Selecione **X Remover atribuições** nas opções na parte superior da caixa de diálogo.
7. Responda **Sim** quando a caixa de confirmação for aberta.
8. Feche a tela.

### Exercício 4 – Importação em massa de usuários

#### Tarefa 1 – Operações em massa para criar usuários com um arquivo .csv

1. No menu do Microsoft Entra ID, primeiro abra **Identidade**, selecione **Usuários** e **Todos os usuários**.

2. No bloco **Usuários | Todos os usuários**, selecione a seta suspensa **Operações em massa** e, em seguida, **Criar em massa**.

3. A seleção de **Criar em massa** abrirá um novo bloco. Esse bloco fornece um link de **Download** de arquivo de modelo que você editará para preencher com suas informações de usuário e carregará para adicionar a criação em massa de usuários.

4. Selecione **Download** para baixar o arquivo .csv.

5. O modelo .csv fornece os campos incluídos com o perfil de usuário. Isso inclui o nome de usuário, o nome de exibição e a senha inicial necessários. Você também pode preencher campos opcionais, como Departamento e Local de Uso, neste momento. A captura de tela a seguir é um exemplo de como você pode completar o arquivo .csv: 

    ![Importação em massa usando a entrada do arquivo csv](./media/bulkimportexample.png)

    Você pode modificar esse arquivo para adicionar usuários em massa.  Observe que você não precisa preencher todo o campo.  De acordo com os dados de amostra fornecidos, você precisa adicionar as informações de nome e nome de usuário.

6. Um CSV de amostra foi fornecido na pasta Allfiles/Lab1 -- **SC300BulkUser.csv**.
   1. Abra o Bloco de Notas.
     - Dentro do ambiente de laboratório, selecione o botão INICIAR e digite Bloco de Notas.  
   1. Abra o arquivo SC300BulkUser.csv
   1. Altere **Inserir seu nome de domínio** para o domínio do seu ambiente de laboratório do Azure.
   1. Salve o arquivo.

7. Na caixa de diálogo **Criar usuários em massa**, selecione o ícone de pasta do arquivo na etapa 3.

8. Procure a pasta Allfiles/Lab1 e selecione o arquivo **SC300BulkUser.csv**.

9. Selecione **Abrir**.

7. Você será notificado de que o arquivo foi carregado com sucesso.Escolha **Enviar** para adicionar os usuários. 

Quando os usuários forem criados, você será avisado de que a criação foi bem-sucedida.  Feche o bloco Criar usuários em massa e os novos usuários serão preenchidos na lista **Usuários | Todos os usuários**. 

#### Tarefa 2 - Adição em massa de usuários usando o PowerShell

1. Abra o PowerShell como administrador.Isso pode ser feito pesquisando o PowerShell no Windows e escolhendo Executar como administrador. 

**Observação** – Você precisa ter o PowerShell versão 7.2 ou superior para que este laboratório funcione.  Quando o PowerShell abrir, você obterá uma versão na parte superior da tela, se você estiver executando e versão mais antiga, siga as instruções na tela para ir para https://aka.ms/PowerShell-Release?tag=7.3.9. Role para baixo até a seção de ativos e selecione powershell-7.3.1-win-x64.msi. Quando o download for concluído, selecione Abrir arquivo. Instale usando todos os padrões.

2. Você precisará instalar o módulo do Microsoft.Graph PowerShell se não o tiver usado antes.  Execute s dois comandos a seguir e confirme a operação quando solicitado apertando Y:

    ```
    Install-Module Microsoft.Graph
    ```
3. Confirme se o módulo do Microsoft.Graph está instalado:

    ```
    Get-InstalledModule Microsoft.Graph
    ```
    

4. Em seguida, você precisará fazer logon no Azure executando:  

    ```
    Connect-MgGraph -Scopes "User.ReadWrite.All"
    ``` 
    O navegador Edge será aberto e solicitaremos que você entre.  Use a conta de Administrador do MOD para se conectar.  Aceite a solicitação de permissões e feche a janela do navegador.

5. Para verificar se você está conectado e ver os usuários existentes, execute:  

    ``` 
    Get-MgUser 
    ```
    
7. Para atribuir uma senha comum temporária a todos os novos usuários, execute o comando a seguir e substitua <Enter a complex Password> pela senha que você gostaria de fornecer aos usuários.  

    ``` 
    $PWProfile = @{
        Password = "<Enter a complex password you will>";
        ForceChangePasswordNextSignIn = $false
    }
    ```

8. Você está pronto para criar novos usuários.  O comando a seguir será preenchido com as informações do usuário e executado.  Se você tiver mais de um usuário para adicionar, poderá usar um arquivo txt do bloco de notas para adicionar as informações e copiar/colar no PowerShell. 

    ```
    New-MgUser `
        -DisplayName "New PW User" `
        -GivenName "New" -Surname "User" `
        -MailNickname "newuser" `
        -UsageLocation "US" `
        -UserPrincipalName "newuser@<labtenantname.com>" `
        -PasswordProfile $PWProfile -AccountEnabled `
        -Department "Research" -JobTitle "Trainer"
    ```
**Observação** - Substitua **labtenantname.com** pelo nome **onmicrosoft.com**atribuído pelo locatário do laboratório.

## Experimente gerenciar usuários

Você pode adicionar e remover usuários com a página do Microsoft Entra ID.  No entanto, usuários podem ser criados e as funções podem ser atribuídas usando o script.  Experimente dar à conta de usuário de Chris Green uma função diferente usando o script. 
 

### Exercício 5 – Remover um usuário do Microsoft Entra ID

#### Tarefa 1 – Remover um usuário

Pode acontecer de uma conta ser excluída e, em seguida, precisar ser recuperada. Você precisa verificar se pode recuperar uma conta que foi excluída recentemente.

1. Navegue até [https://entra.micrososft.com](Microsoft Entra admin center).

2. Na navegação à esquerda, em **Identidade**, selecione **Usuários**.

3. Na lista **Todos usuários**, marque a caixa de seleção para um usuário que será excluído. Por exemplo, selecione **Chris Green**.

    **Dica** - A seleção de usuários na lista permite que você gerencie vários usuários ao mesmo tempo. Se você selecionar o usuário, para abrir a página desse usuário, só estará gerenciando esse usuário individual.

    ![Imagem da tela exibindo a lista Todos os usuários com a caixa de seleção Um usuário selecionada e outra caixa de seleção realçada indicando a capacidade de selecionar vários usuários da lista.](./media/lp1-mod2-remove-user.png)

4. Com a conta de usuário selecionada no menu, selecione **Excluir**.

5. Revise a caixa de diálogo e selecione **Sim**.

#### Tarefa 2 – Restaurar um usuário excluído

1. Na página Usuários, selecione **Todos usuários** na navegação à esquerda e selecione **Usuários excluídos**.

2. Revise a lista de usuários excluídos e selecione **Chris Green**.

    **Importante** - Por padrão, as contas de usuário excluídas são permanentemente removidas do Azure Active Directory automaticamente após 30 dias.

3. No menu, selecione **Restaurar usuário**.

4. Examine a caixa de diálogo e selecione **OK**.

5. No painel de navegação esquerdo, clique em **Todos os usuários**.

6. Verifique se o usuário foi restaurado.


### Exercício 6 - Adicionar uma licença do Windows 10 a uma conta de usuário

#### Tarefa 1 - Localizar seu usuário não licenciado no Azure Active Directory

Algumas contas de usuário em sua organização não receberão todos os produtos disponíveis em sua licença atribuída ou precisarão de atualizações ou adições à atribuição de licença. Você precisa garantir que possa atualizar a atribuição de licença de uma conta de usuário no Microsoft Entra ID.

1. Navegue até [https://entra.microsoft.com]( https://entra.microsoft.com).

2. Na navegação à esquerda, em **Identidade**, selecione **Usuários** e, em seguida, **Todos os usuários**.

3. Na página Usuários, digite **Raul** na caixa de pesquisa.

4. Selecione **Raul Razo**.

5. Revise o perfil de Raul e verifique se ele tem um Local de Uso definido.

    **Aviso** - Para atribuir uma licença a um usuário, um local de uso deve ser atribuído ao usuário.

6. Selecione o item de menu **Licenças** no menu à esquerda.

7. Certifique-se de que Raul esteja com "Nenhuma atribuição de licença encontrada".

8. Navegue de volta para **Todos os Usuários**. Na navegação à esquerda, em **Identidade**, selecione **Usuários**

9. Na página Usuários, selecione **Raul Razo**.

10. No painel de navegação esquerdo, selecione **Licenças**.

11. Selecione o botão **+ Atribuições**. 

12. Na página Atualizar atribuições de licença, marque a caixa de seleção de uma licença do **Windows 10/11 Enterprise E3**.

    ![Imagem da tela exibindo a página Atualizar atribuições de licença e as opções de licença realçadas.](./media/lp1-mod2-assign-user-license-options.png)

13. Ao concluir, selecione **Salvar**.

14. Na parte superior da tela, selecione **Página Inicial**, selecione **Contoso**, **Usuário** e clique em **Raul Razo**.

15. Observe que a licença foi atribuída.
