---
lab:
  title: 18 – Políticas de acesso para o Defender para Aplicativos de Nuvem
  learning path: '03'
  module: Module 03 - Implement Access Management for Apps
---

# 18 – Políticas de acesso e de sessão para o Defender para Aplicativos de Nuvem

### Tipo de logon = administração do Microsoft 365

## Cenário do laboratório

O Microsoft Defender para Aplicativos de Nuvem nos permite criar políticas de Acesso condicional adicionais específicas para os aplicativos de nuvem que estamos monitorando.  A criação dessas políticas pode ser feita no menu Controle no portal do Microsoft Defender para Aplicativos de Nuvem.

#### Tempo estimado: 20 minutos

### Exercício 1 – Criar e testar a política de Controle de Aplicativos de Acesso Condicional

#### Tarefa 1 – Confirmar se o PradeepG tem acesso incondicional ao FORMS

1. Inicie uma nova janela de **navegação InPrivate**.
2. Conecte-se ao [https://forms.microsoft.com](https://forms.microsoft.com).
3. Selecione logon no canto superior direito da página.
4. Faça login como Pradeep Gupta.
   - Nome de usuário = PradeepG@<<<your lab hoster provided domain>>>
   - Senha = a senha da sua guia Recursos
5. Confirme se o Microsoft Forms está abrindo e se você não recebe nenhuma mensagem de aviso.
6. Feche a janela de navegação InPrivate.

#### Tarefa 2 – Configure seu Microsoft Entra ID para trabalhar com o Microsoft Defender para Aplicativos de Nuvem.

1. Navegue até [https://entra.microsoft.com](https://entra.microsoft.com) e vá para Microsoft Entra ID.

2. Em **Identidade**, selecione **Proteção**.

3. Selecione o **Acesso Condicional**.

4. Selecione **+ Criar nova política**.

5. Insira um nome de política, como **Monitorar Pradeep usando formulários**.

6. Em **Atribuições**, escolha **0 usuários e grupos selecionados**, marque **Usuários específicos inclusos** e, em seguida, escolha **Selecionar usuários e grupos**, e marque **Usuários e grupos**.

7. Escolha a conta **Pradeep Gupta** para o locatário do laboratório e marque **Selecionar**.

8. Em **Recursos de destino**, selecione **Nenhum recurso de destino selecionado**.

9. Escolha **Selecionar aplicativos**, em seguida, escolha **Microsoft Forms** e **Selecionar**. 

10. Em **Controles de acesso** selecione **Sessão ** e **0 controles selecionados**.

11. Selecione a caixa **Usar Controle de Aplicativos de Acesso Condicional**, deixe o padrão **Somente monitorar**e escolha **Selecionar**.

12. Em **Habilitar política**, selecione **Ativar** e **Criar**.

#### Tarefa 3 – Fazer logon no Forms e validar se o acesso condicional está monitorando

1. Inicie uma nova janela de **navegação InPrivate**.
2. Conecte-se ao [https://forms.microsoft.com](https://forms.microsoft.com).
3. Selecione logon no canto superior direito da página.
4. Faça login como Pradeep Gupta.
   - Nome de usuário = PradeepG@<<<your lab hoster provided domain>>>
   - Senha = a senha da sua guia Recursos
5. Confirme que o Pradeep tem acesso e que você recebeu uma nova mensagem:
   - Sua empresa está monitorando o uso deste aplicativo.
6. Feche a janela de navegação InPrivate.

### Exercício 2 – Configurar alertas no Microsoft Defender para Aplicativos de Nuvem

#### Tarefa 1 – Acessar o Microsoft Defender para Aplicativos de Nuvem e criar o Controle de Aplicativos de Acesso Condicional

Registrar seu aplicativo estabelece uma relação de confiança entre seu aplicativo e a plataforma de identidade da Microsoft. A confiança é unidirecional: seu aplicativo confia na plataforma de identidade da Microsoft, e não o contrário.

1. Entre no [https://security.microsoft.com](https://security.microsoft.com) usando uma conta de administrador global.

1. No menu à esquerda, role até e selecione **Políticas** na **seção Aplicativos em nuvem** do menu à esquerda.

1. No menu **Políticas**, localize e selecione **Gerenciamento de Políticas**.

1. Selecione **+ Criar política**. Selecione **Política de Acesso**.

1. Insira um nome para a política, como **Monitorar o acesso ao Microsoft Forms.**.

1. Deixe a configuração **Categoria** como **Controle de acesso**.

1. Em **Atividades correspondentes a todos os seguintes**, selecione a lista suspensa para **Em conformidade com Intune, ingressado no Microsoft Entra Hybrid** e desmarque **Ingressado no Microsoft Entra Hybrid**.

1. Selecione a lista suspensa para **Selecionar aplicativos**.  Selecione **Microsoft Forms**.

1. Deixe **Ações** como **Teste**.

1. Em **Alertas**, deixe a opção **Criar um alerta...** marcada e selecione **Enviar alerta como email**.

1. Insira o endereço de email do administrador do laboratório e pressione **Enter** no teclado.

1. Selecione **Criar** para criar a política de acesso.

#### Tarefa 2 – Fazer login como Pradeep no Forms para disparar a atividade

1. Inicie uma nova janela de **navegação InPrivate**.
2. Conecte-se ao [https://forms.microsoft.com](https://forms.microsoft.com).
3. Selecione logon no canto superior direito da página.
4. Faça login como Pradeep Gupta.
   - Nome de usuário = PradeepG@<<<your lab hoster provided domain>>>
   - Senha = a senha da sua guia Recursos
5. Confirme que o Pradeep tem acesso e que você recebeu uma nova mensagem:
   - Sua empresa está monitorando o uso deste aplicativo.
6. Feche a janela de navegação InPrivate.

#### Tarefa 3 – Examinar a atividade no Defender para Aplicativos em Nuvem

1. Retorne ao navegador que execute o Defender para Aplicativos em Nuvem
2. Atualize o navegador para garantir que os dados mais recentes sejam baixados.
3. No menu **Investigar** selecione **Log de atividades**.
4. Usando o **Aplicativo: filtro** selecione **Microsoft Forms** na lista.
5. Observe os registros de logon de Pradeep.
