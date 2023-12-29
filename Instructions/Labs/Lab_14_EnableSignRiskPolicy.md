---
lab:
  title: 14 - Habilitar as políticas de risco de usuários e entradas
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# Laboratório 14 - Habilitar políticas de risco de usuários e entradas

## Cenário do laboratório

Como uma camada adicional de segurança, você precisa habilitar e configurar as políticas de risco de usuários e entradas da organização do Azure AD.

#### Tempo previsto: 10 minutos


### Exercício 1 - Habilitar política de risco de usuário

#### Tarefa 1 - Configurar a política

1. Entre no [https://portal.azure.com]( https://portal.azure.com)usando uma conta de administrador global.

2. Abra o menu do portal e selecione  **Azure Active Directory**.

3. Na página do Azure Active Directory, em **Gerenciar**, selecione **Segurança**.

4. Na página Segurança, na navegação à esquerda, selecione **Identity Protection**.

5. Na página do Identity Protection, na navegação à esquerda, selecione **Política de risco de usuário**.

    ![Imagem da tela exibindo a página de política de risco do usuário e o caminho de navegação realçado](./media/lp2-mod4-browse-to-identity-protection.png)

6. Em **Atribuições**, selecione **Todos os usuários** e examine as opções disponíveis.

7. Você pode selecionar de **Todos os usuários** ou **Selecionar indivíduos e grupos,** se limitar a distribuição.

8. Além disso, você pode optar por excluir usuários da política.

9. Em **Risco do usuário**, selecione **Baixo e superior**.

10. No painel Risco do usuário, selecione **Alto** e, em seguida, selecione **Concluído**.

11. Em **Controles** > **Acesso**, selecione **Bloquear acesso**.

12. No painel de acesso, examine as opções disponíveis.

    Dica**** - A recomendação da Microsoft é permitir o acesso e exigir alteração de senha.

13. Marque a caixa de seleção **Exigir alteração de senha** e depois selecione **Concluído**.

14. Em **Imposição de política**, selecione **Ativar** e **Salvar**.

#### Tarefa 2- Habilitar política de risco de entrada

1. Na página do Identity Protection, na navegação à esquerda, selecione **Política de risco de entrada**.

2. Assim como acontece com a política de Risco do usuário, a política de risco de entrada pode ser atribuída a usuários e grupos e permite que você exclua os usuários da política.

3. Em **Risco de entrada**, selecione **Baixo e superior**.

4. No painel Risco de entrada, selecione **Alto** e depois **Concluído**.

5. Em **Controles** > **Acesso**, selecione **Bloquear acesso**.

6. Marque a caixa de seleção **Exigir autenticação multifator** e selecione **Concluído**.

7. Em **Imposição de política**, selecione **Ativar** e **Salvar**.
