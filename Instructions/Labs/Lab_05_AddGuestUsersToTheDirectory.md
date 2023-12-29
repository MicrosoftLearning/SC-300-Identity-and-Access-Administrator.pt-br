---
lab:
  title: '05: adicionar usuários convidados ao diretório'
  learning path: '01'
  module: Module 01 - Implement an identity management solution
---

# Laboratório 05: Adicionar usuários convidados ao diretório

## Cenário do laboratório

Sua empresa trabalha com muitos fornecedores e, ocasionalmente, você precisa adicionar algumas contas de fornecedor ao seu diretório como convidado.

#### Tempo previsto: 20 minutos

### Exercício 1: adicionar usuários convidados ao diretório

#### Tarefa: adicionar o usuário convidado

1. Faça logon no  [https://portal.azure.com](https://portal.azure.com) como um usuário ao qual foi atribuída uma função do diretório de administrador limitado ou a função Emissor de convites independente.

2. Selecione  **Azure Active Directory**.

3. Em  **Gerenciar**, selecione  **Usuários**.

4. Selecione  **+ Novo usuário**.

5. No menu Novo usuário, selecione **Convidar usuário externo** e adicione suas informações como usuário convidado.

    **OBSERVAÇÃO:** não há suporte para endereços de email de grupo; insira o endereço de email para um indivíduo. Além disso, alguns provedores de email permitem que os usuários adicionem um sinal de adição (+) de símbolo e texto adicional aos seus endereços de email para ajudar com coisas como a filtragem de caixa de entrada. No entanto, o Azure AD não dá suporte para símbolos de adição em endereços de email no momento. Para evitar problemas de entrega, omita o símbolo de adição e quaisquer caracteres seguintes até o símbolo @.

6. Insira um endereço de email, como **sc300externaluser1@sc300email.com**.

7. Ao concluir, selecione **Convidar**.

8. Na página Usuários, verifique se sua conta está listada e, na coluna **Tipo de usuário**, verifique se **Convidado** é mostrado.

Depois de enviar o convite, a conta de usuário é automaticamente adicionada ao diretório como convidado.


### Exercício 2: convidar usuários convidados em massa

#### Tarefa 1: convite de usuários em massa

Uma parceria recente foi estabelecida com outra empresa. Por enquanto, os funcionários da empresa parceira serão adicionados como convidados. É necessário garantir que você possa importar vários usuários convidados de uma só vez.

1. Entre no [https://portal.azure.com](https://portal.azure.com) como Administrador global.

2. No painel de navegação, selecione **Azure Active Directory**.

3. Em **Gerenciar**, selecione **Usuários**.

4. Na página Usuários, no menu, selecione **Operações em massa > Convite em massa**.

     ![Imagem da tela exibindo a página Todos os usuários com as opções Em massa e convite e as opções de menu de Convite em massa realçadas](./media/lp1-mod3-bulk-invite-option.png)

5. No painel de usuários do convite em massa, selecione **Baixar** para um modelo CSV de exemplo com propriedades de convite.

6. Usando um editor para exibir o arquivo CSV, examine o modelo.

7. Abra o modelo .csv e adicione uma linha para cada usuário convidado. Os valores obrigatórios são:

    - **Endereço de email a ser convidado** – o usuário que receberá um convite
    - **URL de redirecionamento** – a URL para a qual o usuário convidado é encaminhado depois de aceitar o convite.

    ![Imagem da tela exibindo o CSV de exemplo do modelo de convidados em massa](./media/lp1-mod3-template-csv.png)

8. Salve o arquivo.

9. Na página Convidar usuários em massa, em **Carregar o arquivo CSV**, procure o arquivo.

     **Observação:** quando você selecionar o arquivo, a validação do arquivo .csv será iniciada.

10. Após a validação do conteúdo do arquivo, você verá a mensagem **Arquivo carregado com êxito**. Se houver erros, você precisará corrigi-los antes de enviar o trabalho.

    ![Imagem da tela exibindo usuários convidados em massa com o arquivo carregado com êxito realçado](./media/lp1-mod3-bulk-invite-users-upload-csv.png)

11. Quando o arquivo passar na validação, selecione **Enviar** para iniciar a operação em massa do Azure que adiciona os convites.

12. Para exibir o status do trabalho, clique em **Selecione aqui para exibir o status de cada operação**. Se preferir, selecione **Resultados da operação em massa** na seção Atividade. Para obter detalhes de cada item de linha na operação em massa, escolha os valores nas colunas **Nº de Êxitos**, **Nº de Falhas** ou **Total de Solicitações**. Se ocorrerem falhas, os motivos da falha serão listados.

    ![Imagem da tela exibindo os resultados de uma operação em massa](./media/lp1-mod3-bulk-operations-results.png)

13. Quando o trabalho for concluído, você verá uma notificação indicando que a operação em massa foi bem-sucedida.

#### Tarefa 2: convidar usuários convidados com o PowerShell

1. Abra o PowerShell como administrador.  Faça isso pesquisando o PowerShell no Windows e escolhendo Executar como administrador.  

1. Você precisará adicionar o módulo do PowerShell do Azure AD se ainda não tiver usado ele.  Execute o comando do: Install-Module AzureAD.  Quando solicitado, selecione "S" para continuar.

    ``` 
    Install-Module AzureAD
    ```

1. Confirme se o módulo foi instalado corretamente executando o comando:  

    ```
    Get-Module AzureAD 
    ```

1. Em seguida, você precisará fazer logon no Azure executando:  

    ```
    Connect-AzureAD
    ```
    
1. A janela de logon da Microsoft aparecerá para você fazer logon no Azure AD.  

1. Para verificar se você está conectado e ver os usuários existentes, execute:  

    ```
    Get-AzureADUser 
    ```

1. Está tudo pronto para convidar um usuário convidado.  O comando a seguir será preenchido com as informações do usuário e executado.  Se você tiver mais de um usuário para adicionar, poderá usar um arquivo txt do Bloco de notas para adicionar as informações e copiar/colar no PowerShell. 

    ```
    New-AzureADMSInvitation -InvitedUserDisplayName "Display" -InvitedUserEmailAddress name@emaildomain.com -InviteRedirectURL https://myapps.microsoft.com -SendInvitationMessage $true 
    ```

Agora você sabe como convidar usuários no portal do Azure AD e no Centro de administração do Microsoft 365, enviar convites em massa com um arquivo csv e convidar usuários com comandos do PowerShell.
