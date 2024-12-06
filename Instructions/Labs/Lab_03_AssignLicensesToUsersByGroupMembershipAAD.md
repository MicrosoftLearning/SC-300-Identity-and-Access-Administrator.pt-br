---
lab:
  title: 03 - Atribuir licenças usando associação de grupo
  learning path: '01'
  module: Module 01 - Implement an identity management solution
---

# Laboratório 03: atribuir licenças usando associação de grupo

### Tipo de logon = administração do Microsoft 365

## Cenário do laboratório

Sua organização decidiu usar grupos de segurança no Microsoft Entra ID para gerenciar licenças. Você precisa configurar um novo grupo de segurança e atribuir uma licença a esse grupo e verificar se as licenças de membros do grupo foram atualizadas.

#### Tempo estimado: 25 minutos

### Exercício 1 - Criar um grupo de segurança e adicionar um usuário

#### Tarefa 1 - Verificar se Delia Dennis tem acesso ao Office 365

1. Inicie uma nova janela do navegador InPrivate.
2. Conecte-se ao [https://www.office.com](https://www.office.com).
3. Selecione Entrar e conecte-se como Delia Dennis.

   | **Configuração**| **Valor**|
   | :--- | :--- |
   | Nome de Usuário | DeliaD@`your domain name.com`|
   | Senha| Digite a senha do Administrador Global nos Recursos|

4. Você deve se conectar ao site da Office.com, mas verá uma mensagem indicando que não tem uma licença.

   ![Imagem da tela do site Office.com com Delia Dennis logada, mas nenhum aplicativo do Office está disponível, porque nenhuma licença está atribuída.](./media/delia-no-office-license.png)
    
5. Feche a janela do navegador.

#### Atefa 2 - Criar um grupo de segurança em Microsoft Entra ID

1. Navegue até [https://entra.microsoft.com](https://entra.microsoft.com).

2. No painel de navegação esquerdo, em **Identidade**, selecione **Grupos**, e depois selecione **Todos os Grupos**.
3. Na página Grupos, no menu, selecione **Novo grupo**.
4. Crie um grupo com as seguintes informações:

   | **Configuração**| **Valor**|
   | :--- | :--- |
   | Tipo de grupo| Segurança|
   | Nome do grupo| sg-SC300-O365|
   | Tipo de afiliação| Atribuído|
   | Proprietários| *Atribuir sua própria conta de administrador como o proprietário do grupo*|

5. Selecione o texto **Nenhum membro selecionado** em Membros.
6. Selecione **Delia Dennis** na lista de usuários.
7. Escolha o botão **Selecionar**.

   ![Imagem da tela exibindo a página Novo Grupo com Tipo de grupo, Nome do grupo, Proprietários e Membros realçados.](./media/lp1-mod2-create-group.png)

8. Selecione o botão **Criar**.
9. Ao concluir, verifique se o grupo chamado **sg-SC300-O365** é mostrado na lista **Todos os grupos**.

#### Tarefa 3 – Adicionar uma licença do Office ao sg-SC300-O365

Você precisa adicionar e remover licenças por meio do Centro de administração do Microsoft 365. Esta é uma mudança relativamente nova.

1. Abra uma nova guia no navegador.

2. Conecte-se ao centro de administração do Microsoft 365 em http://admin.microsoft.com.

3. Faça login como sua conta de administrador, se solicitado.

4. No menu à esquerda, selecione **Cobrança** e, em seguida, selecione **Licenças**.

5. Selecione Licença do **Office 365 E3** na lista.

6. Escolha a guia **Grupos** na tela de licenças.

7. Escolha o item **+ Adicionar licença**.

8. Procure pelo grupo **sg-SC300-O365** e selecione-o na lista.

8. Depois de adicionar Raul, clique em **Atribuir**.
 
9. Feche a mensagem de confirmação.

10. Volte para a guia do navegador com o **Centro de administração do Microsoft** aberto.

11. Navegue de volta para **Todos os grupos**. Na navegação à esquerda, em **Identidade**, selecione **Grupos**

12. Na página Usuários, selecione **sg-SC300-O365**.

13. No painel de navegação esquerdo, selecione **Licenças**.

14. Observe que a licença do Office 365 E3 foi atribuída.

15. Você pode sair da tela de licença.

#### Taks 4 - Confirmar a licença do Office 365

1. Inicie uma nova janela do navegador InPrivate.
2. Conecte-se ao [https://www.office.com](https://www.office.com).
3. Selecione Entrar e conecte-se como Delia Dennis.

   | **Configuração**| **Valor**|
   | :--- | :--- |
   | Nome de Usuário | DeliaD@`your domain name.com`|
   | Senha| Digite a senha do Administrador Global nos Recursos|

4. Você deve se conectar ao site da Office.com e não ver nenhuma mensagem sobre a licença. Todos os aplicativos do Office estão disponíveis à esquerda.

   ![Imagem de tela do site Office.com com Delia Dennis logada com aplicativos de escritório disponíveis, porque uma licença está atribuída.](./media/delia-office-license.png)
    
5. Feche a janela do navegador. 

### Exercício 2 – Criar um grupo do Microsoft 365 no Microsoft Entra ID

#### Tarefa 1 - Criar o grupo

Parte de suas funções como administrador do Microsoft Entra é criar diferentes tipos de grupos. Você precisa criar um novo grupo do Microsoft 365 para o departamento de vendas da sua organização.

1. Navegue até [https://entra.microsoft.com]( https://entra.microsoft.com).

2. No painel de navegação esquerdo, em **Identidade**, selecione **Grupos**, e depois selecione **Todos os Grupos**.

3. Na página Grupos, no menu, selecione **Novo grupo**.

4. Crie um grupo com as seguintes informações:

   | **Configuração**| **Valor**|
   | :--- | :--- |
   | Tipo de grupo| Microsoft 365|
   | Nome do grupo| Vendas do noroeste|
   | Tipo de afiliação| Atribuído|
   | Proprietários| *Atribuir sua própria conta de administrador como o proprietário do grupo*|
   | Membros| **Alex Wilber** e **Bianca Pisani**|

   ![Imagem da tela exibindo a página Novo Grupo com Tipo de grupo, Nome do grupo, Proprietários e Membros realçados.](./media/lp1-mod2-create-o365-group.png)

5. Ao concluir, verifique se o grupo chamado **Vendas no noroeste** é mostrado na lista **Todos os grupos**.

### Exercício 3 - Criar um grupo dinâmico com todos os usuários como membros

#### Tarefa 1 - Criar o grupo dinâmico

À medida que sua empresa cresce, o gerenciamento manual de grupos é muito demorado. Desde a padronização do diretório, agora você pode aproveitar os grupos dinâmicos. Você deve criar um novo grupo dinâmico para garantir que esteja pronto para a criação de grupos dinâmicos em produção.

1. Entre no[https://entra.microsoft.com](https://entra.microsoft.com) com uma conta que é atribuída à função de Administrador global ou de Administrador de usuários no locatário.

2. Selecionar **Identidade**.

3. Em **Grupos**, selecione **Todos os grupos** e selecione **Novo grupo**.

4. Na página novo grupo, em **Tipo de grupo**, selecione **Segurança**.

5. Na caixa **Nome do grupo**, digite **SC300-myDynamicGroup**.

6. Selecione o menu **Tipo de afiliação** e, em seguida, selecione **Usuário dinâmico**.

7. Selecione um **Proprietário** para o grupo.

7. Em **Membros dinâmicos do usuário**, selecione **Adicionar consulta dinâmica**.

8. No lado direito acima da caixa **Sintaxe de regra**, selecione **Editar**.

9. No painel Editar sintaxe de regra, insira a seguinte expressão na caixa **Sintaxe de regra**:

   ```powershell
   user.objectid -ne null
   ```

   **Aviso** - o `user.objectid` diferencia maiúsculas de minúsculas.

10. Selecione **OK**. A regra é exibida na caixa Sintaxe de regra.

   ![Imagem da tela exibindo a página de regras de associação de grupo dinâmico com sintaxe de regra realçada.](./media/lp1-mod3-dynamic-group-membership-rule.png)

11. Selecione **Salvar**. O novo grupo dinâmico agora incluirá usuários convidados B2B, assim como usuários membros.

12. Na página Novo grupo, selecione **Criar** para criar o grupo.

#### Tarefa 2 - Verificar se os membros foram adicionados

**Nota** - A associação de grupo dinâmica pode demorar até 15 minutos.

1. Selecione na **Página inicial**`Microsoft Entra admin center`.
2. Inicie o **Identidade**.
3. No menu **Grupos**, selecione em **Todos os grupos**.
4. Na caixa de filtro, digite **SC300** e seu grupo recém-criado será listado.
5. Selecione em **SC300-myDynamicGroup** para abrir o grupo.
6. Observe que ele mostra que contém mais de 30** Membros diretos*.
7. No menu **Gerenciar**, selecione **Membros**.
8. Revise os membros.

#### Tarefa 3 - Experimente regras alternativas

1. Tente criar um grupo apenas com usuários **Convidados**:

   - (user.objectid -ne null) e (user.userType -eq "Guest")

2. Tente criar um grupo com apenas **membros** dos usuários do Microsoft Entra.

   - (user.objectid -ne null) e (user.userType -eq "Member")
