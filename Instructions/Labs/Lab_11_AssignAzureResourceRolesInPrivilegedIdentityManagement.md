---
lab:
  title: 11 –Atribuir funções de recurso do Azure no Privileged Identity Management
  learning path: '02'
  module: Module 02 - Implement an authentication and access management solution
---

# Laboratório 11 – Atribuir funções de recurso do Azure no Privileged Identity Management

### Tipo de logon = logon do recurso do Azure

## Cenário do laboratório

O Microsoft Entra Privileged Identity Management (PIM) pode gerenciar as funções de recurso internas do Azure, bem como funções personalizadas, incluindo (dentre outras):

- Proprietário
- Administrador de Acesso do Usuário
- Colaborador
- Administrador de Segurança
- Gerenciador de Segurança

Você precisará tornar um usuário qualificado para uma função de recurso do Azure.

#### Tempo estimado: 10 minutos

### Exercício 1 – PIM com recursos do Azure

#### Tarefa 1 – Atribuir funções de recurso do Azure

1. Entre no [https://entra.microsoft.com](https://entra.microsoft.com) usando a conta de administrador fornecida.

2. Pesquise e selecione o **Privileged Identity Management.**

3. Na página Privileged Identity Management, no painel de navegação esquerdo, selecione **Recursos do Azure.**

**Dica de laboratório** – As próximas etapas são escritas para a experiência de Recurso do Azure herdado.  Você pode mudar para a experiência antiga na parte superior da tela ou concluir o exercício na nova experiência sem o passo a passo.

4. No menu suspenso Assinaturas, escolha o item Assinatura do MOC##### . Em seguida, na parte inferior da tela, selecione **Gerenciar recursos**.

5. Na página Recursos do Azure – Descoberta, selecione sua assinatura.

6. Na página **Visão geral**, revise as informações.

   ![Imagem da tela exibindo o Recurso do Azure adicionado recentemente](./media/lp4-mod3-pim-az-resource-overview.png)

   **Dica de laboratório** — Devido à natureza do ambiente de laboratório, você não verá nenhum recurso. Consulte a imagem para ver um exemplo.

7. No menu de navegação esquerdo, em **Gerenciar**, selecione **Funções** para ver a lista de funções para recursos do Azure.

8. No menu superior, selecione **+ Adicionar atribuições**.

9. No painel Adicionar atribuições, selecione o menu **Selecionar função** e, depois, **Colaborador do serviço de Gerenciamento de API.**

10. Em **Selecionar membro(s)**, escolha **Nenhum membro selecionado**.

11. Em Selecionar um membro ou grupo, pesquise suas funções de administrador **User1-######@LODSPRODMCA.onmicrosoft.com** da sua organização que receberá a função.  Em seguida, escolha **Selecionar**.

12. Selecione **Avançar**.

13. Na guia **Configurações**, em **Tipo de atribuição**, selecione **Qualificado**.

   - Atribuições **Qualificadas** exigem que o membro da função execute uma ação para usar a função. As ações podem incluir a execução de uma verificação de Autenticação multifator (MFA), fornecimento de uma justificativa comercial ou solicitação de aprovação dos aprovadores designados.

   - As atribuições **Ativas** não exigem que o membro execute nenhuma ação para usar a função. Membros atribuídos como ativos sempre têm os privilégios atribuídos à função.

14. Para especificar uma duração de atribuição, altere as datas e os horários de início e término.

15. Quando terminar, selecione **Atribuir**.

16. Depois que a nova atribuição de função for criada, uma notificação de status será exibida.

#### Tarefa 2 – Atualizar ou remover uma atribuição de função de recurso

**Observação** — Devido à segurança imposta neste ambiente de laboratório, você não pode concluir essas etapas.  Revise as etapas na interface do usuário, mas você não poderá aplicar alterações.  Estamos trabalhando ativamente para resolver isso.

Siga estas etapas para atualizar ou remover uma atribuição de função existente.

1. Abra o **Microsoft Entra Privileged Identity Management**.

2. Selecione **Recursos do Azure**.

3. Selecione a assinatura que você deseja gerenciar para abrir sua página de visão geral.

4. Em **Gerenciar**, selecione **Atribuições**.

5. Na guia **Atribuições qualificadas**, na coluna Ação, examine as opções disponíveis.

6. Selecione **Remover**.

7. Na caixa de diálogo **Remover**, analise as informações e selecione **Sim**.
