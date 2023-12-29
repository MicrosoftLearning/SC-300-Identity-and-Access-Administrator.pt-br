---
lab:
  title: 18 - Políticas de acesso para Defender para Aplicativos de Nuvem
  learning path: '03'
  module: Module 03 - Implement Access Management for Apps
---

# 18 - Defender para Aplicativos de Nuvem – Políticas de acesso e de sessão

## Cenário do laboratório

O Microsoft Defender para Aplicativos de Nuvem permite criar políticas de Acesso Condicional adicionais específicas para os aplicativos de nuvem que estamos monitorando.  A criação dessas políticas pode ser feita no menu Controle no portal do Microsoft Defender para Aplicativos de Nuvem.

#### Tempo previsto: 20 minutos

### Exercício 1 - Criar e testar a política de Controle de Aplicativo de Acesso Condicional

#### Tarefa 1 - Confirmar se o PradeepG tem acesso incondicional ao FORMS

1. Inicie uma nova janela de **Navegação anônima**.
2. Conecte-se ao [https://forms.microsoft.com](https://forms.microsoft.com).
3. Selecione o logon no canto superior direito da página.
4. Faça login como Pradeep Gupta.
   - Nome de usuário = PradeepG@<<<your lab hoster provided domain>>>
   - Senha = a senha da guia Recursos
5. Confirme se o Microsoft Forms é aberto e se você não recebe nenhuma mensagem de aviso.
6. Feche a janela de navegação anônima.

#### Tarefa 2- Configure o Azure AD para trabalhar com o Defender para Aplicativos de Nuvem

1. Navegue até o [portal.azure.com](portal.azure.com) e acesse Azure Active Directory.

2. Em **Gerenciar**, selecione **Segurança**.

3. Em **Proteger**, selecione **Acesso Condicional**.

4. Selecione no menu suspenso **+ Nova política** e depois **Criar política**.

5. Insira o nome de uma política, como **Monitorar o Pradeep usando Forms**.

6. Em **Usuários ou identidades de carga de trabalho**, selecione **Usuários específicos incluídos** e depois **Selecionar usuários e grupos** e marque **Usuários e grupos**.

7. Escolha a conta **Pradeep Gupta** para o locatário do laboratório e selecione **Selecionar**.

8. Em **Aplicativos de nuvem ou ações**, selecione **Nenhum aplicativo de nuvem, ação ou contextos de autenticação selecionados**.

9. Selecione **Selecionar aplicativos**, depois **Microsoft Forms** e, por fim, **Selecionar**. 

10. Em **Controles de acesso**, selecione **sessão** e ** 0 controles selecionados**.

11. Selecione a caixa **Usar controle de aplicativo de Acesso Condicional**, deixe o padrão **Somente monitorar** e selecione **Selecionar**.

12. Em **Habilitar política**, selecione **Ativa** e depois **Criar**.

#### Tarefa 3 - Fazer login em Forms e validar se o acesso condicional está monitorando

1. Inicie uma nova janela de **Navegação anônima**.
2. Conecte-se ao [https://forms.microsoft.com](https://forms.microsoft.com).
3. Selecione o logon no canto superior direito da página.
4. Faça login como Pradeep Gupta.
   - Nome de usuário = PradeepG@<<<your lab hoster provided domain>>>
   - Senha = a senha da guia Recursos
5. Confirme se Pradeep tem acesso e se você recebe uma nova mensagem:
   - Sua empresa está monitorando o uso deste aplicativo.
6. Feche a janela de navegação anônima.

### Exercício 2 - Configurar alertas no Microsoft Defender para Aplicativos de Nuvem

#### Tarefa 1 - Acessar o Microsoft Defender para Aplicativos de Nuvem e criar Controle de Aplicativos de Acesso Condicional

Registrar seu aplicativo estabelece uma relação de confiança entre seu aplicativo e a plataforma de identidade da Microsoft. A confiança é unidirecional: seu aplicativo confia na plataforma de identidade da Microsoft, e não o contrário.

1. Entre no [https://security.microsoft.com](https://security.microsoft.com)usando uma conta de administrador global.

1. No menu esquerdo, role até a parte inferior e selecione **Mais recursos**.

1. Na janela **Mais recursos**, localize e selecione **Abrir** em **Microsoft Defender para Aplicativos de Nuvem**.  Isso vai levá-lo ao portal do **Microsoft Defender para Aplicativos de Nuvem ** na conta do Microsoft 365.

1. No menu do portal **Microsoft Defender para Aplicativos de Nuvem**, selecione a seta suspensa para **Controle** e selecione **Políticas**.

1. Selecione **+ Criar política**. Selecione **Políticas de acesso**.

1. Insira um nome para a política, como **Monitorar o acesso ao Microsoft Forms**.

1. Deixe a **Categoria** como **Controle de acesso**.

1. Em **Atividades correspondentes a todos os itens a seguir**, selecione a lista suspensa para  **Intune compatível, Hybrid Azure AD ingressou** e desmarque **Hybrid Azure AD ingressou**.

1. Selecione o menu suspenso **Selecionar aplicativos**.  Selecione **Microsoft Forms**.

1. Deixe **Ações** como **Testar**.

1. Em **Alertas**, deixe a opção **Criar um alerta...** marcada e selecione **Alerta enviado como e-mail**.

1. Insira o endereço de e-mail do administrador do laboratório e selecione **Enter** no teclado.

1. Selecione **Criar** para criar a política de acesso.

#### Tarefa 2 - Faça login como Pradeep no Forms para acionar a atividade

1. Inicie uma nova janela de **Navegação anônima**.
2. Conecte-se ao [https://forms.microsoft.com](https://forms.microsoft.com).
3. Selecione o logon no canto superior direito da página.
4. Faça login como Pradeep Gupta.
   - Nome de usuário = PradeepG@<<<your lab hoster provided domain>>>
   - Senha = a senha da guia Recursos
5. Confirme se Pradeep tem acesso e se você recebe uma nova mensagem:
   - Sua empresa está monitorando o uso deste aplicativo.
6. Feche a janela de navegação anônima.

#### Tarefa 3 - Revisar a Atividade no Defender para Aplicativos de Nuvem

1. Retorne ao navegador que executa o Defender para Aplicativos de Nuvem.
2. Atualize o navegador para garantir que os dados mais recentes sejam baixados.
3. No menu **Investigar**, selecione **Log de atividade**.
4. Usando o **Aplicativo: filtro** escolher **Microsoft Forms** da lista.
5. Observe os registros de logon para Pradeep.
