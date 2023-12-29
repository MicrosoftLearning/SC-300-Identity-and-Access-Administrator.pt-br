---
lab:
  title: 15 - Configurar a política de registro com autenticação multifator do Azure AD
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# Laboratório 15 - Configurar a política de registro com autenticação multifator do Azure AD

## Cenário do laboratório

A autenticação multifator do Azure AD fornece um meio para verificar quem você é usando mais do que apenas um nome de usuário e senha. Ela oferece uma segunda camada de segurança para entradas de usuário. Para que usuários sejam capazes de responder a solicitações de MFA, eles devem se registrar primeiro para Autenticação multifator do Azure AD. Você deve configurar a política de registro de MFA da organização do Azure AD para ser atribuída a todos os usuários.

#### Tempo previsto: 10 minutos

### Exercício 1 - Configurar a política de registro de MFA

#### Tarefa 1 - Configuração da política

1. Entre no [https://portal.azure.com]( https://portal.azure.com)usando uma conta de administrador global.

2. Abra o menu do portal e selecione  **Azure Active Directory**.

3. Na página do Azure Active Directory, em **Gerenciar**, selecione **Segurança**.

4. Na página Segurança, na navegação à esquerda, selecione **Identity Protection**.

5. Na página do Identity Protection, na navegação à esquerda, em **Proteger**, selecione **Politica de registro com autenticação multifator**.

    ![Imagem da tela exibindo a página da política de registro de MFA com o caminho de navegação realçado](./media/lp2-mod4-browse-to-mfa-registration-policy.png)

6. Em **Atribuições**

7. Em **Atribuições**, selecione **Todos os usuários** e examine as opções disponíveis.

8. Você pode selecionar de **Todos os usuários** ou **Selecionar indivíduos e grupos,** se limitar a distribuição.

9. Além disso, você pode optar por excluir usuários da política.

10. Em **Controles**, observe que a seção **Exigir registro de MFA do Azure AD** está selecionada e não pode ser alterada.


#### Tarefa 2 - Configurar a política do Azure AD Identity Protection para registro de MFA

**Observação**: O Azure AD Identity Protection requer uma licença do Azure AD Premium P2 para ser ativado. 

1. No portal do Azure, navegue até **Azure AD Identity Portection **na barra de pesquisa.

1. Em **Proteger** no menu, selecione **Política de registro de MFA**.

1. Em **Atribuições**, selecione **Todos os usuários ** e selecione um usuário para impor MFA.

1. Altere **a imposição da política** de **Desativada** para **Ativada**.

1. Selecione **Salvar**.

Isso exigirá que o usuário conclua o registro de MFA na próxima vez que tentar fazer login.

1. Em um navegador privado, navegue até `https://login.microsoftonline.com`. Insira o nome de usuário e senha do locatário.  Observe os requisitos adicionais de informações de segurança que o usuário é solicitado a inserir.
