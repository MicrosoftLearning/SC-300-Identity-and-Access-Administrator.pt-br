---
lab:
  title: '06: adicionar um provedor de identidade federado'
  learning path: '01'
  module: Module 01 - Implement an identity management solution
---

# Laboratório 06: adicionar um provedor de identidade federado

## Cenário do laboratório

Sua empresa trabalha com muitos fornecedores e, ocasionalmente, você precisa adicionar algumas contas de fornecedor ao seu diretório como convidado e permitir que eles usem sua Conta do Google para entrar.

#### Tempo previsto: 25 minutos

### Exercício 1 - Configurar provedores de identidade

#### Tarefa 1: configurar o Google para ser usado como um provedor de identidade

**Observação importante:** para este exercício, você precisará de uma conta do Gmail no Google. Crie uma **nova Conta do Google** e siga as etapas para realizar o exercício.  Certifique-se de anotar o endereço de email e senha, eles são necessários para completar o laboratório.

1. Acesse as APIs do Google em https://console.developers.google.com e entre com sua conta do Google. É recomendável que você use uma conta do Google de equipe compartilhada.

2. Aceite os termos de serviço se você for solicitado a fazê-lo.

**Criar um novo projeto:**
3. Na parte superior da página, selecione o menu do projeto para abrir a página Selecionar um projeto. Escolha **Novo projeto**.  Mantenha os campos restantes com as configurações padrão.

4. Na página Novo projeto, dê um nome ao projeto (por exemplo, **MyB2BApp**) e selecione **Criar**.

5. Abra o novo projeto selecionando o link na caixa de mensagem de Notificações ou usando o menu Projeto na parte superior da página.

6. No menu à esquerda, selecione **APIs e serviços**, e em seguida, selecione a **tela de consentimento do OAuth**.

7. Em Tipo de usuário, selecione **Externo** e, em seguida, selecione **Criar**.

8. Na **tela de consentimento do OAuth**, em Informações do aplicativo, insira um Nome de aplicativo, como **Azure AD**.

9. Em email de suporte do usuário, selecione um endereço de email. Isso deve incluir o endereço de email que você usou para fazer logon no Google.

10. Em Domínios autorizados, selecione **+ Adicionar domínio** e, em seguida, adicione o domínio microsoftonline.com.

   ```
   microsoftonline.com
   ```

11. Em Informações de contato do desenvolvedor, insira o endereço de email da conta de laboratório que você usou para entrar no portal.

12. Selecione **Salvar e continuar**.

13. No menu esquerdo, selecione **Credenciais**.

14. Selecione **+ Criar credenciais** e, em seguida, selecione **ID do cliente OAuth**.

15. No menu tipo de aplicativo, selecione Aplicativo Web. Dê ao aplicativo um nome adequado, como B2B do Azure AD. Em **URIs de redirecionamento autorizados**, adicione os seguintes URIs:

   ```
      https://login.microsoftonline.com
   ```
      https://login.microsoftonline.com/te/**tenant ID**/oauth2/authresp    (onde <tenant ID> está o ID do locatário)
   ```
      https://login.microsoftonline.com/te/**tenant name**.onmicrosoft.com/oauth2/authresp
       (where <tenant name> is your tenant name)
   ```

16. Selecione **Criar**. Copie o **ID do cliente** e o **segredo do cliente**. Você os usará quando adicionar o provedor de identidade no portal do Azure.

17. Você pode deixar seu projeto em um status de publicação de Teste.

#### Tarefa 2: adicionar um usuário de teste
18. Selecione a **tela de consentimento do OAuth** no menu APIs e serviços.

19. Na seção **Testar usuários* da página, escolha **+ Adicionar usuários**.

20. Insira a conta do Gmail que você criou (ou está usando) para este laboratório.

21. Selecione **Salvar**


### Exercício 2: configurar o Azure para trabalhar com um provedor de identidade externo

#### Tarefa 1: configurar o Azure AD para a federação do Google
1. Entre no [https://portal.azure.com](https://portal.azure.com) como administrador.

2. Selecione  **Azure Active Directory**.

3. Em **Gerenciar**, selecione  **Identidades externas**.

4. Escolha **Todos os provedores de identidade** no menu à esquerda.

5. A Microsoft fornece uma federação direta para o **Google** como um provedor de identidade.  Isso pode ser iniciado selecionando **+ Google** na página **Identidades externas | Todos os provedores de identidade**
 
6. Depois de selecionar + Google, outra página será aberta com informações adicionais necessárias para configurar o Google como um provedor de identidade.  

7. Insira o **ID do cliente** e o **Segredo do cliente** obtidos anteriormente.

8. Selecione **Salvar**.

Isso conclui a configuração do Google como um provedor de identidade.

#### Tarefa 2: convidá-lo a testar a conta de usuário
9. Se você usou uma conta existente do Gmail, lembre-se de excluir a conta com **Identidades externas | Todos os provedores de identidade**. Você também pode retornar ao console do desenvolvedor do Google e excluir o projeto que criou.

10. Abra o Azure Active Directory (Azure AD).

11. Vá para Usuários.

12. Selecione **+ Novo usuário**.

13. Selecione **Convidar usuário externo** no menu suspenso.

14. Insira as informações da conta do Gmail que você configurou como usuário de teste para o Google App no Exercício 1, Tarefa 2.

15. Insira uma mensagem pessoal como desejar.

16. Selecione **Convidar**.

#### Tarefa 3: aceitar o convite e fazer logon
17. Use um navegador anônimo para fazer logon em sua conta do Gmail.

18. Abra o **Convite da Microsoft em nome de** na caixa de entrada.

19. Selecione o link **Aceitar convite** na mensagem.

20. Insira seu nome de usuário e senha conforme solicitado na caixa de diálogo de logon (se solicitado).
   **OBSERVAÇÃO** se a federação estiver funcionando corretamente, é aqui que você verá os primeiros resultados do seu novo provedor de identidade externo do Google.  Você irá para a tela de logon e poderá fazer logon com suas credenciais do Gmail.  Se a federação não estiver funcionando ou não tiver sido configurada, o usuário receberá um email de VERIFICAÇÃO DE CONTA após o logon, para confirmar a conta.  Com a federação, não é necessária nenhuma verificação adicional.

   **OBSERVAÇÃO** Se você receber um erro de acesso 500, aguarde cerca de 30 segundos e atualize a página.  Escolha REENVIAR.  Esse erro é um problema de tempo somente no ambiente de laboratório.

21. Leia a nova mensagem **Permissões solicitadas por:** que você recebe.  Essa mensagem vem do seu Domínio de laboratório do Azure.

22. Escolha **Aceitar**.

23. Assim que o logon estiver concluído, você receberá MyApplications.

#### Tarefa 4: fazer logon no Microsoft 365 usando sua conta do Google
24. Depois de concluir o processo de convite de usuário externo da Tarefa 3, você poderá fazer logon diretamente no Microsoft Online.

25. Abra uma nova guia no navegador que você abriu.
   **OBSERVAÇÃO** se você não abriu um novo navegador anônimo na Tarefa 3, deverá fazê-lo nesta etapa.

26. Insira o seguinte endereço da Web:

   ```
   login.microsoftonline.com
   ```

27. Selecione **Opções de entrada** no diálogo.
 
28. Escolha **Entrar em uma organização**.

29. Insira o **nome de domínio do locatário do laboratório** na caixa e selecione **Avançar**.

30. Insira o endereço de email e a senha do **Google** que você criou.
Nesse momento, você deverá ver sua conta ser passada para o Google para confirmação; em seguida, entre no portal do Microsoft Office.
