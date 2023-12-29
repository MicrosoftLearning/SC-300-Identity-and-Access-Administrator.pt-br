---
lab:
  title: '09: habilitar a redefinição de senha self-service do Azure AD'
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# Laboratório 09: configurar e implantar a redefinição de senha self-service
## Cenário do laboratório

A empresa decidiu capacitar os funcionários e habilitar a redefinição de senha self-service. Você deve definir essa configuração em sua organização.

#### Tempo previsto: 15 minutos

### Exercício 1: criar um grupo com a SSPR habilitado e adicionar usuários a ele

#### Tarefa 1: criar um grupo ao qual atribuir a SSPR

Você quer distribuir a SSPR para um conjunto limitado de usuários primeiro para verificar se a configuração da SSPR funciona conforme o esperado. Você irá criar um grupo de segurança para a distribuição limitada e adicionar um usuário ao grupo.

1. Na página Azure Active Directory, em **Gerenciar**, selecione **Grupos** e selecione **Novo grupo** na janela do lado direito.

2. Crie um novo grupo com as seguintes informações:

    | **Configuração**| **Valor**|
    | :--- | :--- |
    | Tipo de grupo| Segurança|
    | Nome do grupo| SSPRTesters|
    | Descrição do grupo| Usuários de teste da distribuição da SSPR|
    | Tipo de afiliação| Atribuído|
    | Membros| Alex Wilber |
    | |  Allan Deyoung |
    | | Bruna Alves |
  
    
3. Selecione **Criar**.

    ![Imagem da tela exibindo a página Novo grupo com Tipo de grupo, Nome do grupo e Criar realçados](./media/lp2-mod2-create-sspr-security-group.png)

#### Tarefa 2: habilitar a SSPR para seu grupo de teste

Habilite a SSPR para o grupo.

1. Navegue de volta à página do Azure Active Directory.

2. Em **Gerenciar**, selecione  **Redefinição de senha**.

3. Na página Propriedades da página Redefinição de senha, em **Redefinição de senha self-service habilitada**, selecione  **Selecionado**.

4. Selecione **Selecionar grupo** e escolha **SSPRSecurityGroupUser**.

5. No painel Política de redefinição de senha padrão, selecione o grupo **SSPRTesters** .

6. Na página Propriedades da página Redefinição de senha, selecione  **Salvar**.

    ![Imagem da tela exibindo a página de propriedades Redefinição de senha com Selecionado, Selecionar grupo e Salvar realçados](./media/lp2-mod2-enable-password-reset-for-selected-group.png)

7. Em  **Gerenciar**, selecione Revisar os valores padrão das configurações de  **Métodos de autenticação**,  **Registro**, **Notificações** e **Personalização**.

    **Observação**: é importante ter o **telefone** selecionado como um dos métodos de autenticação para o restante deste laboratório, mas você também pode ter outras opções.

#### Tarefa 3: registrar-se na SSPR com Alex

Agora que a configuração da SSPR foi concluída, registre um número do telefone celular para o usuário que você criou.

1. Abra um navegador diferente ou uma sessão anônima do navegador e acesse [https://aka.ms/ssprsetup](https://aka.ms/ssprsetup).

    Isso garante que seja solicitada a você a autenticação de usuário.

2. Entre como **AlexW@** `<<organization-domain-name>>.onmicrosoft.com` com a senha = Insira a senha de administrador do locatário (Consulte a guia Recursos de laboratório para recuperar a senha de administrador).

    **Observação:** substitua organization-domain-name pelo nome de seu domínio.

3. Se for solicitado a atualizar sua senha, insira uma nova senha de sua escolha. Não se esqueça de registrar a nova senha.

4. Na caixa de diálogo **Mais informações necessárias**, selecione **Avançar**.

5. Na página Manter sua conta segura, use a opção **Telefone**.

    ![Imagem da tela exibindo a página Manter sua conta segura com a caixa de diálogo Escolher um método diferente realçada](./media/lp2-mod2-keep-your-account-secure-page.png)

    **Observação:** neste laboratório, você usará a opção **Telefone**. Insira os detalhes de seu celular.

6. Insira seu número de celular pessoal no campo de número de telefone.
7. Selecione  **Enviar código por SMS**.
8. Selecione **Avançar**.

9. Ao receber o código em seu celular, insira-o na caixa de texto e selecione **Avançar**.

10. Depois do registro de seu telefone, selecione **Avançar** e depois **Concluído**.

11. Feche o navegador. Você não precisa concluir o processo de entrada.

#### Tarefa 4: testar SSPR

Agora, vamos testar se o usuário pode redefinir a própria senha.

1. Abra um navegador diferente ou uma sessão anônima do navegador e acesse  [https://portal.azure.com](https://portal.azure.com).

    Isso garante que seja solicitada a você a autenticação de usuário.

2. Insira **AlexW@** `<<organization-domain-name>>.onmicrosoft.com` e depois selecione **Avançar**.

    **Observação:** substitua organization-domain-name pelo nome de seu domínio.

3. Na página Inserir senha, selecione **Esqueci minha senha**.

4. Na página Voltar para sua conta, preencha as informações solicitadas e selecione **Avançar**.

    ![Imagem da tela exibindo a página Voltar para sua conta com Email ou nome de usuário, a caixa de captcha e o botão Avançar realçados](./media/lp2-mod2-get-back-into-your-account-page.png)

5. Na tarefa da **Etapa 1 da verificação**, selecione **Enviar SMS para meu celular**, insira seu número de telefone e selecione **Enviar SMS**.

    ![Imagem da tela exibindo a etapa de verificação 1 com os métodos de contato, a caixa de número de telefone e o botão Enviar SMS realçados](./media/lp2-mod2-sspr-verification-step-1.png)

6. Insira seu código de verificação e selecione **Avançar**.

7. Na etapa Escolher nova senha, insira e confirme sua nova senha.  Recomende uma senha = **Pass@w.rd1234**.

8. Ao concluir, selecione **Concluir**.

9. Entre como **AlexW** com a nova senha que você criou.

10. Insira seu código de verificação e verifique se você pode concluir o processo de entrada.

11. Depois de terminar, feche o navegador.

#### Tarefa 5: o que acontecerá se você testar um usuário que não esteja no grupo SSPRTesters?

1. Como teste, abra uma nova janela do navegador anônimo e tente fazer logon no Portal do Azure como GradyA e selecione a opção **Esqueci minha senha**.
