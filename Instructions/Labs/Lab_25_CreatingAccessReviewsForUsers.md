---
lab:
  title: 25 – Criar revisões de acesso para usuários internos e externos
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Laboratório 25: criar revisões de acesso para usuários internos e externos

### Tipo de logon = administração do Microsoft 365

## Cenário do laboratório

O acesso privilegiado do usuário deve ser revisado regularmente de maneira semelhante. Como se trata de atribuições de acesso elevado, a revisão delas deve ser feita de forma consistente, conforme identificado pela empresa.Atribuições privilegiadas não utilizadas e desnecessárias devem ser removidas.A remoção automatizada também deve ser configurada para usuários que não estão mais na empresa ou mudaram de departamento dentro da empresa.

#### Tempo estimado: 5 minutos

### Exercício 1 – Criar uma revisão interna do acesso

#### Tarefa – Criar uma nova revisão de acesso

1. Entre no  [https://entra.microsoft.com](https://entra.microsoft.com) como um Administrador global.

2. As revisões de acesso podem gerenciar o ciclo de vida do acesso.Em **Microsoft Entra ID**, localize **Governança de Identidade** e selecione **Revisões de acesso**.

3. Selecione **+ Nova revisão de acesso**.

4. Na caixa **Selecionar o que revisar**, escolha **Equipes + Grupos**.

5. Selecione **Selecionar Equipes + grupos**, escolha o grupo **Vendas e Marketing** na lista e clique em **Selecionar**.

6. Defina o **Escopo** como **Todos os usuários**.

7. Selecione **Avançar: revisões** para prosseguir no assistente.

8. O próximo passo é determinar os revisores.Esses revisores podem ser os próprios membros, fazendo uma autorrevisão, ou sendo atribuídos a supervisores, ao revisarem o acesso de um departamento inteiro. Você também pode definir a ação quando um revisor não responder para remover automaticamente esse acesso privilegiado do membro.

9. Escolha um revisor, **Alex Wilber**, e revise a opção de recorrência **Anual**.  Em seguida, selecione **Avançar: configurações**.

10. As configurações avançadas permitem que você insira uma mensagem como parte da revisão.

11. Alterne para a guia **Avançar: Revisar + Criar** para finalizar a revisão de acesso.

12. Nomeie a revisão de acesso **Teste de revisão de acesso SC300**.

13. Selecione **Criar** na parte inferior da página.

    **Observação** – Quando a revisão de acesso for criada, a lista de revisão de acesso será preenchida com as funções e os proprietários das revisões.

14. Os membros que estão sendo revisados receberão um email quando a revisão for iniciada.

15. A seleção da revisão de acesso de uma das funções fornecerá o status dessa revisão de acesso.
