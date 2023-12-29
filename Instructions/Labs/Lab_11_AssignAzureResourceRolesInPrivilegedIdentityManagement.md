---
lab:
  title: '11: atribuir funções de recurso do Azure no Privileged Identity Management'
  learning path: '02'
  module: Module 02 - Implement an authentication and access management solution
---

# Laboratório 11: atribuir funções de recurso do Azure no Privileged Identity Management

**Observação** - Este laboratório requer um Azure Pass. Consulte o laboratório 00 para obter instruções.

## Cenário do laboratório

O PIM (Privileged Identity Management) do Azure AD (Azure Active Directory) pode gerenciar as funções de recurso do Azure internas, bem como as funções personalizadas, incluindo (mas não se limitando a):

- Proprietário
- Administrador de Acesso do Usuário
- Colaborador
- Administrador de Segurança
- Gerenciador de Segurança

Você precisa tornar um usuário elegível para uma função de recurso do Azure.


#### Tempo previsto: 10 minutos

### Exercício 1: PIM com recursos do Azure AD

#### Tarefa 1: atribuir funções de recurso do Azure

1. Entre no [https://portal.azure.com](https://portal.azure.com)usando uma conta de administrador global.

2. Pesquise e selecione o **Azure AD Privileged Identity Management.**

3. Na página Privileged Identity Management, no painel de navegação esquerdo, selecione **Recursos do Azure**.

4. No menu superior, selecione **Descobrir recursos**.

5. Na página Recursos do Azure – Descobrir, selecione sua assinatura e, no menu superior, selecione **Gerenciar recurso**.

   ![Imagem da tela exibindo a página Descobrir recursos do Azure com a assinatura e o recurso de gerenciamento realçados](./media/lp4-mod3-pim-azure-resource-management.png)

6. Na caixa de diálogo **Integração do recurso selecionado para gerenciamento**, analise as informações e selecione **OK**.

7. Quando a integração for concluída, feche o painel Recursos do Azure – Descobrir.

8. Na página de recursos do Azure, selecione a assinatura.

   ![Imagem da tela exibindo o Recurso do Azure adicionado recentemente](./media/lp4-mod3-pim-az-resource-overview.png)

9. No menu de navegação esquerdo, em **Gerenciar**, selecione **Funções** para ver a lista de funções para recursos do Azure.

10. No menu superior, selecione **+ Adicionar atribuições**.

11. Na página Adicionar atribuições, selecione o menu **Selecionar função** e, depois, **Colaborador do serviço de Gerenciamento de API**.

12. Em **Selecionar membro(s)**, escolha **Nenhum membro selecionado**.

13. Selecione **Miriam Graham** na sua organização que será atribuída à função.  Em seguida, escolha **Selecionar**.

14. Selecione **Avançar**.

15. Na guia **Configurações**, em **Tipo de atribuição**, selecione **Qualificado**.

   - Atribuições **Qualificadas** exigem que o membro da função execute uma ação para usar a função. As ações podem incluir a execução de uma verificação de Autenticação multifator (MFA), fornecimento de uma justificativa comercial ou solicitação de aprovação dos aprovadores designados.

   - As atribuições **Ativas** não exigem que o membro execute nenhuma ação para usar a função. Membros atribuídos como ativos sempre têm os privilégios atribuídos à função.

16. Para especificar uma duração de atribuição, altere as datas e os horários de início e término.

17. Quando terminar, selecione **Atribuir**.

18. Depois que a nova atribuição de função for criada, uma notificação de status será exibida.

#### Tarefa 2: atualizar ou remover uma atribuição de função de recurso existente

Siga estas etapas para atualizar ou remover uma atribuição de função existente.

1. Abra o **Azure AD Privileged Identity Management**.

2. Selecione **Recursos do Azure**.

3. Selecione a assinatura que você deseja gerenciar para abrir sua página de visão geral.

4. Em **Gerenciar**, selecione **Atribuições**.

5. Na guia **Funções qualificadas**, na coluna Ação, examine as opções disponíveis.

6. Selecione **Remover**.

7. Na caixa de diálogo **Remover**, analise as informações e selecione **Sim**.
