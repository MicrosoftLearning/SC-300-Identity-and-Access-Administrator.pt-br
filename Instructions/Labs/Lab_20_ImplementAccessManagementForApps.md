---
lab:
  title: '20 – Implementar o gerenciamento de acesso para aplicativos '
  learning path: '03'
  module: Module 03 - Implement Access Management for Apps
---

# Laboratório 20 – Implementar o gerenciamento de acesso para aplicativos

### Tipo de logon = administração do Microsoft 365

## Cenário do laboratório

Sua organização exige que apenas usuários ou grupos específicos tenham acesso a aplicativos empresariais. Você deve atribuir um usuário a um aplicativo específico.

#### Tempo estimado: 5 minutos

### Exercício 1 – Configurar um aplicativo empresarial

#### Tarefa 1 – Adicionar um aplicativo ao locatário do Microsoft Entra

1. Entre no  [https://entra.microsoft.com](https://entra.microsoft.com) usando a conta de Administrador fornecida.

2. Olhe para o menu no lado esquerdo da tela.

3. No menu Identidade, em **Aplicativos**, selecione **Aplicativos empresariais**.

4. No painel Aplicativos empresariais, selecione **+ Novo aplicativo**.

    ![Imagem da tela exibindo a página Aplicativos empresariais com Novo aplicativo realçado](./media/lp3-mod1-new-enterprise-application.png)

5. Na página Procurar na Galeria do Microsoft Entra, na caixa **Pesquisar aplicativo**, insira **GitHub**.

    ![Imagem da tela exibindo a página Procurar na Galeria do Microsoft Entra com a caixa de pesquisa realçada](./media/lp3-mod1-azure-ad-gallery-search.png)

6. Nos resultados, selecione **GitHub Enterprise Cloud – conta corporativa**.

7. Em **GitHub Enterprise Cloud – conta corporativa**, examine as configurações e selecione **Criar**.

8. Quando a conta for criada, haverá o redirecionamento para a página GitHub Enterprise Cloud – Conta Enterprise.

#### Tarefa 2 – Atribuir usuários a um aplicativo

1. Na página GitHub Enterprise Cloud – Conta Enterprise, em Visão geral, na **Introdução**, selecione **1. Atribuir usuários e grupos**.

2. Como alternativa, na navegação à esquerda, em **Gerenciar**, você pode selecionar **Usuários e grupos**.

3. Na página Usuários e grupos, no menu, selecione **+ Adicionar usuário/grupo**.

4. Na página Adicionar Atribuição, na seção **Usuários e grupos**, selecione **Nenhum selecionado**.

5. No painel Usuários e grupos, selecione Adele Vance a sua conta de administrador MOD.

6. Escolha **Selecionar**.

    ![Imagem da tela exibindo a adição de uma atribuição de conta de usuário a um aplicativo com o botão Selecionar realçado ](./media/lp3-mod1-add-app-assignment.png)

7. Selecione **Atribuir**.

