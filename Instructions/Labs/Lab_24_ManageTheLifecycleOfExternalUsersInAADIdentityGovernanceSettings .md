---
lab:
  title: 24 - Gerencie o ciclo de vida de usuários externos nas configurações da Governânça do Microsoft Entra Identity
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Laboratório 24:gerencie o ciclo de vida de usuários externos nas configurações da Governança do Microsoft Entra Identity.  

## Cenário do laboratório

Você pode selecionar o que acontece quando um usuário externo, que foi convidado para seu diretório por meio de uma solicitação de pacote de acesso que está em aprovação, não tiver mais nenhuma atribuição de pacote de acesso. Isso pode ocorrer se o usuário ceder todas as atribuições de pacote de acesso ou se a última atribuição de pacote de acesso dele expirar. Por padrão, quando um usuário externo não tem mais nenhuma atribuição de pacote de acesso, ele é impedido de entrar no seu diretório. Após 30 dias, a conta de usuário convidado dele é removida do seu diretório.

#### Tempo estimado: 5 minutos

### Exercício 1 – Configurações da Governança de Identidade do Microsoft Entra

#### Tarefa 1 – Gerencie o ciclo de vida de usuários externos nas configurações da Governança do Microsoft Entra Identity

1. Entre no  [https://entra.microsoft.com](https://entra.microsoft.com) como um Administrador global.

2. Abra o item do Microsoft Entra ID e selecione  **Governança de Identidade**.

3. No menu de navegação à esquerda, em **Gerenciamento de direitos**, selecione **Configurações**.

4. No menu superior, selecione **Editar**.

    ![Imagem da tela exibindo a página de configurações de governança de identidade com a opção de gerenciar o ciclo de vida de usuários externos realçada.](./media/lp4-mod1-manage-lifcycle-of-ext-users.png)

5. Na seção **Gerenciar o ciclo de vida de usuários externos**, analise as diferentes configurações para usuários externos.

6. Quando um usuário externo perde a última atribuição a qualquer pacote de acesso, se você quiser impedi-lo de entrar nesse diretório, defina **Impedir que o usuário externo entre nesse diretório** como **Sim**.

7. Se um usuário estiver impedido de entrar no diretório, então ele não poderá solicitar novamente o pacote de acesso nem solicitar acesso adicional nesse diretório. Não impeça o usuário de entrar caso posteriormente ele vá precisar solicitar acesso a outros pacotes de acesso.

8. Depois que um usuário externo perder a última atribuição a qualquer pacote de acesso, se você quiser remover a conta de usuário convidado dele nesse diretório, defina **Remover usuário externo** como **Sim**.

    **Observação** – O gerenciamento de direitos remove apenas as contas que foram convidadas por meio do gerenciamento de direitos. Além disso, observe que um usuário será impedido de entrar e removido desse diretório, mesmo que ele tenha sido adicionado a recursos desse diretório que não eram atribuições de pacote de acesso. Se o convidado estava no diretório antes de receber atribuições de pacote de acesso, ele permanecerá. Porém, se o convidado foi convidado por meio de uma atribuição de pacote de acesso e, depois de ser convidado também foi atribuído a um site do OneDrive for Business ou do SharePoint Online, ele ainda será removido.

9. Se você quiser remover a conta de usuário convidado nesse diretório, poderá definir o número de dias antes de ela ser removida. Se você quiser remover a conta de usuário convidado assim que o usuário perder a última atribuição a qualquer pacote de acesso, defina **Número de dias antes de remover o usuário externo desse diretório** como **0**.

10. Selecione **Salvar** sempre que fizer alterações.
