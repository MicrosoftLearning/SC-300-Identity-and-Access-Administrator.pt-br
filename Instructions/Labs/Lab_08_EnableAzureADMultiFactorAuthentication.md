---
lab:
  title: 08 – Habilitar a autenticação multifator
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# Laboratório 08 – Habilitar a autenticação multifator

## Cenário do laboratório

Para aprimorar a segurança em sua organização, você recebeu a direção para habilitar a autenticação multifator para o Microsoft Entra ID.

#### Tempo estimado: 15 minutos

**IMPORTANTE** – Uma licença premium do Microsoft Entra ID é necessária para este exercício.

### Exercício 1 – Revisar e habilitar a Autenticação Multifator no Azure

#### Tarefa 1 – Revisar as opções da Autenticação Multifator do Azure

1. Navegue até [https://entra.microsoft.com](https://entra.microsoft.com) e entre usando uma Conta de administrador global para o diretório.

2. Use o recurso de pesquisa e procure por **multifator**.

3. Nos resultados da pesquisa, selecione **Autenticação multifator**.

    Como alternativa, você pode abrir **Identidade**, selecionar **Proteção** e clicar em **Autenticação multifator**.

4. Na página Introdução, em **Configurar**, selecione **Configurações adicionais de MFA baseadas em nuvem**.

    ![Captura de tela mostrando as opções do MFA no painel](./media/lp2-mod1-set-additional-mfa-settings.png)

5. Na nova página do navegador, você pode ver as opções de MFA para usuários do Azure e configurações de serviço.

    ![Captura de tela mostrando a configuração do MFA](./media/lp2-mod1-mfa-settings.png)

    É aqui em que você selecionaria os métodos de autenticação com suporte; na tela acima, todos eles estão selecionados.

    Você também pode habilitar ou desabilitar senhas de aplicativos aqui, o que permite aos usuários criar senhas de conta exclusivas para aplicativos que não dão suporte à autenticação multifator. Esse recurso permite que o usuário se autentique com a identidade do Microsoft Entra usando uma senha diferente específica desse aplicativo.

#### Tarefa 2 – Configurar regras de acesso condicional para MFA para Delia Dennis

Em seguida, vamos examinar como configurar regras de política de acesso condicional que impõem a MFA para usuários convidados que acessam aplicativos específicos na sua rede.

1. Volte para o centro de administração do Microsoft Entra, selecione **Identidade**, depois **Proteção** e, em seguida, **Acesso condicional**.

2. No menu, selecione **+ Nova política**. No menu suspenso, selecione **+ Criar nova política**.

    ![Captura de tela destacando o botão Nova Política no centro de administração do Microsoft Entra.](./media/lp2-mod1-azure-ad-conditional-access-policy.png)

3. Nomeie sua política, por exemplo **MFA_de_Delia**.

4. Em Atribuições, selecione **Usuários ou identidades de carga de trabalho**.

    - Selecione **0 usuários ou identidades de carga de trabalho selecionados**  
    - Na tela do lado direito, marque a caixa de seleção **Selecionar usuários e grupos** para configurar.
    - Marque **Usuários e grupos** (os usuários disponíveis serão preenchidos à direita)
    - Escolha **Delia Dennis** na lista de usuários e clique no botão **Selecionar** .

5. Em Recursos de destino, selecione **Nenhum recurso de destino selecionado**.

   - Na lista suspensa, verifique se **Aplicativos de nuvem** está selecionado.
   - Em Incluir, marque **Todos os aplicativos de nuvem** e observe o aviso que aparece sobre a possibilidade de bloquear-se. 
   - Agora, em Incluir, altere sua escolha para o item **Selecionar aplicativos**.
   - Na caixa de diálogo recém-aberta, escolha **Office 365**.
      - **Lembrete** – em um laboratório anterior, demos a Delia Dennis uma licença do Office 365 e fizemos logon para garantir que funcionava.
   - Escolha **Selecionar**.

6. Examine a seção Condições.

   - Selecione **Locais** e o configure para **Qualquer local**.

7. Em **Controles de Acesso**, encontre a seção **Conceder** e selecione **0 controles selecionados**.

8. Marque a caixa de seleção **Exigir autenticação multifator** para impor a MFA.

9. Certifique-se de que **Exigir todos os controles selecionados** esteja selecionado.

10. Escolha **Selecionar**.

11. Defina **Habilitar política** como **Ativo**.

12. Selecione **Criar** para criar a política.

    ![Captura de tela mostrando a caixa de diálogo completa Adicionar Política](./media/lp2-mod1-conditional-access-new-policy-complete.png)

    A MFA agora está habilitada para o usuário e aplicativo(s) selecionados. Na próxima vez em que um convidado tentar entrar nesse aplicativo, ele deverá se registrar na MFA.

#### Tarefa 3 – Testar o login de Delia

1. Abra uma nova janela de Navegação InPrivate.
2. Conecte-se ao https://www.office.com.
3. Selecione a opção Entrar.
4. Digite **DeliaD@**`<<your domain address>>`.
5. Digite a senha = Digite a senha de administrador global do locatário (Observação: consulte a guia "Recursos de laboratório" para recuperar a senha de administrador).

**Observação** – Neste momento uma das duas coisas vai acontecer.  Você vai receber uma mensagem informando que precisa configurar o aplicativo Authenticator e se registrar na MFA.  Siga as instruções para concluir usando seu telefone pessoal.  OBSERVAÇÃO – há uma chance de que você pode receber uma mensagem de falha de logon com várias opções sobre como prosseguir.  Selecione a opção **Tentar novamente** neste caso.

Você pode ver que, devido à regra de Acesso Condicional que criamos para Delia, a MFA é necessária para iniciar a página inicial do Office 365.

### Exercício 2 – Configurar a MFA para ser necessária para o logon

#### Tarefa 1 – Configurar a MFA do Microsoft Entra por usuário

Por fim, vamos examinar como configurar a MFA para contas de usuário. Essa é outra maneira de acessar as configurações de autenticação multifator.

1. Volte para o centro de administração do Microsoft Entra e localize o menu de navegação à esquerda do Indentity.

2. Selecione **Usuários** e, em seguida, selecione **Todos os usuários**.

3. Na parte superior do painel Usuários, selecione **MFA por usuário**.

   ![Captura de tela mostrando a opção de MFA](./media/lp2-mod1-users-mfa.png)

4. Uma nova guia/janela do navegador será aberta com uma caixa de diálogo de configurações do usuário de autenticação multifator.

   Você pode habilitar ou desabilitar a MFA por usuário, selecionando um deles e, em seguida, usando as etapas rápidas no lado direito.

   ![Captura de tela mostrando as opções de MFA](./media/lp2-mod1-mfa-service-settings-and-users.png)

5. Selecione **Adele Vance** com uma marca de seleção.
6. Selecione a opção **Ativar** em etapas rápidas.
7. Leia o pop-up de notificação, se o receber, e selecione **ativar botão de autenticação multifator**.
8. Selecione **Fechar**.
9. O status da MFA de Adele agora é **Habilitado**.
10. Você pode selecionar as **configurações de serviço** para ver a tela de configuração de MFA, vista anteriormente no laboratório.
11. Feche a guia Configuração de MFA.

#### Tarefa 2 – Tentar fazer login como Adele

1. Se você quiser ver outro exemplo de processo de login da MFA, você pode tentar fazer login como Adele.
