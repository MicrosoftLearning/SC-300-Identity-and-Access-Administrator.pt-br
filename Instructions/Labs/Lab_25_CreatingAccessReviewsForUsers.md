---
lab:
  title: 25 - Criação de revisões de acesso para usuários internos e externos
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Laboratório 25 - Criação de revisões de acesso para usuários internos e externos  

## Cenário do laboratório

O acesso privilegiado do usuário deve ser revisado regularmente de maneira semelhante.Como se trata de atribuições de acesso elevado, a revisão delas deve ser feita de forma consistente, conforme identificado pela empresa.Atribuições privilegiadas não utilizadas e desnecessárias devem ser removidas.A remoção automatizada também deve ser configurada para usuários que não estão mais na empresa ou mudaram de departamento dentro da empresa.

#### Tempo previsto: 5 minutos

### Exercício 1 - Criar uma revisão de acesso interno

#### Tarefa - Criar uma revisão de acesso

1. Entre no  [https://portal.azure.com](https://portal.azure.com) como administrador global.

2. As revisões de acesso podem gerenciar o ciclo de vida do acesso.No **Azure Active Directory**, localize **Identity Governance** no menu **Gerenciar**.  No **Identity Governance**, selecione **Revisões de acesso**.

3. Selecione **+ Nova revisão de acesso**.

4. Na caixa **Selecionar o que examinar** escolha **Equipes + Grupos** do menu suspenso.

5. Selecione **Selecionar equipes + grupos** e escolha o grupo **Vendas e Marketing** na lista e clique em **Selecionar**.

6. Defina o **Escopo** como **Todos os usuários**.

7. Selecione a opção **Revisões** para prosseguir no assistente.

8. O próximo passo é determinar os revisores.Esses revisores podem ser o próprio membro a fazer uma autorrevisão ou as revisões podem ser atribuídas a supervisores se revisarem o acesso de um departamento inteiro. Você também pode definir a ação quando um revisor não responder para remover automaticamente esse acesso privilegiado do membro.

9. Escolha um revisor e a opção de recorrência de revisão.  Em seguida, selecione **Configurações**.

10. As configurações avançadas permitem que você coloque uma mensagem como parte da revisão.

11. Selecione **Examinar e criar** para finalizar a revisão de acesso.

12. Nomeie a revisão de acesso **Teste de revisão de acesso SC300**.

13. Selecione **Criar**. Quando a revisão de acesso for criada, a lista de revisão de acesso será preenchida com as funções e os proprietários das revisões.

14. Os membros que estão em revisão receberão um e-mail quando esta for iniciada.

15. A seleção de uma revisão de acesso de uma das funções fornecerá status nessas revisões de acesso.
