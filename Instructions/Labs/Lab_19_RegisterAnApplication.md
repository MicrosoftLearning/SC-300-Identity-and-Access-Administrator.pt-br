---
lab:
  title: 19 – Registrar um aplicativo
  learning path: '03'
  module: Module 03 - Implement Access Management for Apps
---

# Laboratório 19 - Registrar um aplicativo

#### Tempo previsto: 30 minutos

### Exercício 1 - Registrar um aplicativo

#### Tarefa 1 - Registrar aplicativo

Registrar seu aplicativo estabelece uma relação de confiança entre seu aplicativo e a plataforma de identidade da Microsoft. A confiança é unidirecional: seu aplicativo confia na plataforma de identidade da Microsoft, e não o contrário.

1. Entre no [https://portal.azure.com](https://portal.azure.com) usando uma conta de administrador global.

2. Abra o menu do portal e selecione  **Azure Active Directory**.

3. No **painel do Azure Active Directory**, em **Gerenciar**, selecione **Registros de aplicativo**.

4. Na página **Registros de aplicativo**, no menu, selecione **+ Novo registro**.

5. No painel **registrar um aplicativo**, registre um aplicativo chamado **Aplicativo de demonstração** usando os valores padrão. Não é preciso inserir o URI de redirecionamento.

    ![Imagem da tela exibindo o painel Registrar um aplicativo com o nome e as configurações padrão realçadas](./media/lp3-mod3-register-an-application.png)

6. Ao concluir, você será direcionado para a folha do **Aplicativo de demonstração**.


#### Tarefa 2 - Configurar a plataforma

As configurações para cada tipo de aplicativo, incluindo URIs de redirecionamento, são definidas em  **Configurações de plataforma**  no portal do Azure. Algumas plataformas, como  **Web**  e  **Aplicativos de página única**, exigem que você especifique manualmente um URI de redirecionamento. Para outras plataformas, como dispositivos móveis e desktop, você pode selecionar entre URIs de redirecionamento gerados para você ao definir as outras configurações.

Para definir as configurações do aplicativo com base na plataforma ou no dispositivo que você está direcionando:


1. Adicione e modifique URIs de redirecionamento para seus aplicativos registrados configurando suas definições de plataforma.

1. Selecione seu aplicativo em  **Registros de aplicativo** no portal do Azure.

2. Em  **Gerenciar**, selecione  **Autenticação**.

3. Em  **Configurações da plataforma**, selecione  **+ Adicionar uma plataforma**.

4. Em  **Configurar plataformas**, selecione o bloco para o tipo de aplicativo (plataforma) para definir suas configurações.

    ![Captura de tela do painel Configuração da plataforma no portal do Azure](./media/configure-platforms.png)

    | Plataforma| Definições de configuração|
    | :--- | :--- |
    | Web| Insira um  **URI de redirecionamento**  para seu aplicativo, o local para o qual a plataforma de identidade da Microsoft redireciona o cliente do usuário e envia tokens de segurança após a autenticação. Selecione essa plataforma para aplicativos Web padrão que são executados em um servidor.|
    | Aplicativo de página única| Insira um  **URI de redirecionamento**  para seu aplicativo, o local para o qual a plataforma de identidade da Microsoft redireciona o cliente do usuário e envia tokens de segurança após a autenticação. Selecione esta plataforma se você está criando um aplicativo Web do lado do cliente em JavaScript ou com uma estrutura como Angular, Vue.js, React.js ou Blazor WebAssembly.|
    | iOS/macOS| Insira a  **ID do Pacote** do aplicativo, encontrada no XCode em  *Info.plist*  ou nas Configurações de Build. Um URI de redirecionamento é gerado para você quando você especifica uma ID do Pacote.|
    | Android| Insira o  **Nome do pacote** do aplicativo, que pode ser encontrado no arquivo AndroidManifest.xml, e gere e insira o  **Hash de assinatura**. Um URI de redirecionamento é gerado para você quando você especifica essas configurações.|
    | Aplicativos móveis e para desktop| Selecione um dos  **URIs de redirecionamento sugeridos**  ou especifique um  **URI de redirecionamento personalizado**. Para aplicativos desktop, recomendamos: [https://login.microsoftonline.com/common/oauth2/nativeclient](https://login.microsoftonline.com/common/oauth2/nativeclient). Selecionar essa plataforma para aplicativos móveis que não estão usando a MSAL (Biblioteca de Autenticação da Microsoft) mais recente ou que não estão usando um agente. Selecione também essa plataforma para aplicativos de desktop.|

5. Selecione  **Configurar**  para concluir a configuração da plataforma.

#### Tarefa 3 - Adicionar credenciais, certificado e segredo do cliente

As credenciais são usadas por aplicativos cliente confidenciais que acessam uma API Web. O aplicativos Web, outras APIs da Web e aplicativos de tipo de serviço e de daemon são exemplos de clientes confidenciais. As credenciais permitem que seu aplicativo se autentique como ele mesmo, sem nenhuma interação com um usuário no runtime.

Você pode adicionar certificados e segredos do cliente (uma cadeia de caracteres) como credenciais ao registro do aplicativo cliente confidencial.

![Captura de tela do portal do Azure que mostra o painel Certificados e segredos no registro de aplicativo](./media/portal-05-app-reg-04-credentials.png)


>**Observação**: Chamados às vezes de  *chave pública*, os certificados são os tipos de credenciais recomendados, pois fornecem um nível mais alto de segurança do que um segredo do cliente. Ao usar um certificado público confiável, é possível adicionar o certificado usando o recurso Certificados e segredos. O certificado deve ser um desses tipos de arquivo: .cer, .pem, .crt.


>**Observação**: O segredo do cliente, também conhecido como  *senha do aplicativo*, é um valor de cadeia de caracteres que seu aplicativo pode usar no lugar de um certificado para se identificar. O segredo do cliente é o mais fácil de usar dos dois tipos de credenciais. Geralmente é usado durante o desenvolvimento, mas é considerado menos seguro do que um certificado. Você deve usar certificados em seus aplicativos executados em produção.

1. Selecione seu aplicativo em  **Registros de aplicativo**  no portal do Azure.

2. Selecione  **Certificados e segredos** e, em seguida,  **+ Novo segredo do cliente**.

3. Adicione uma descrição para o segredo do cliente.

4. Selecione uma duração.

5. Selecione **Adicionar**.

6. **Salve o valor do segredo no bloco de notas**  para uso no código do aplicativo cliente; A página Certificados e segredos exibirá o novo valor do segredo. É importante copiar esse valor, pois ele é mostrado apenas uma vez. Se você sair da página e voltar, ela apenas mostrará como um valor mascarado.

1. Ignore as seções  **Adicionar um URI de redirecionamento**  e  **Definir as configurações de plataforma** . Você não precisa configurar um URI de redirecionamento para uma API Web, pois nenhum usuário está conectado interativamente.

1. Ignore a seção  **Adicionar credenciais**  por enquanto. Sua API somente precisará das próprias credencias caso ela acesse uma API downstream, mas esse cenário não é abordado neste artigo.

Com sua API Web registrada, você está pronto para adicionar os escopos que o código da API pode usar para fornecer permissão granular aos consumidores de sua API.


#### Tarefa 5 - Adicionar um escopo

O código em um aplicativo cliente solicita permissão para executar operações definidas por sua API Web passando um token de acesso junto com suas solicitações para o recurso protegido (a API Web). A API Web executará a operação solicitada somente se o token de acesso recebido contiver os escopos (também conhecidos como permissão de aplicativo) necessários para a operação.

Primeiro, siga estas etapas para criar um escopo de exemplo chamado Employees.Read.All:

1. Entre no portal do Azure.

2. Se você tem acesso a vários locatários, use o filtro  **Diretório + assinatura**  no menu superior para selecionar o locatário que contém o registro do aplicativo cliente.

3. Selecione  **Azure Active Directory** > **Registros de aplicativo** e o registro do aplicativo da API.

4. Selecione  **Expor uma API**, depois  **+ Adicionar um escopo**.

    ![Um registro de aplicativo expõe um painel de API no portal do Azure](./media/portal-02-expose-api.png)

5. Você será solicitado a definir um  **URI da ID de aplicativo** se ainda não tiver configurado um. O URI da ID do aplicativo atua como o prefixo dos escopos que você fará referência no código da API e deve ser globalmente exclusivo. Você pode usar o valor padrão fornecido que está no formato api://\<application-client-id\>, ou especificar um URI mais legível, como  `https://contoso.com/api`.

6. Selecione **Salvar e continuar**.

6. Em seguida, especifique os atributos do escopo no painel  **Adicionar um escopo**. Para este passo a passo, você pode usar os valores de exemplo ou especificar o seu próprio valor.

    | Campo| Descrição| Exemplo|
    | :--- | :--- | :--- |
    | Nome do escopo| O nome do seu escopo. Uma convenção comum de nomenclatura de escopo é resource.operation.constraint.| Employees.Read.All|
    | Quem pode consentir| Se esse escopo pode ser consentido por usuários ou se é necessário ter o consentimento do administrador. Selecione Somente administradores para permissões com privilégios mais elevados.| Administradores e usuários|
    | Nome de exibição de consentimento do administrador| Uma breve descrição da finalidade do escopo que somente os administradores verão.| Acesso somente leitura aos registros de funcionários|
    | Descrição do consentimento do administrador| Uma descrição mais detalhada da permissão concedida pelo escopo que somente os administradores verão.| Permitir que o aplicativo tenha acesso somente leitura a todos os dados de funcionários.|
    | Nome de exibição do consentimento do usuário| Uma breve descrição da finalidade do escopo. Mostrado para os usuários somente se você definir Quem pode consentir como Administradores e usuários.| Acesso somente leitura aos registros de funcionários|
    | Descrição de consentimento do usuário| Uma descrição mais detalhada da permissão concedida pelo escopo. Mostrado para os usuários somente se você definir Quem pode consentir como Administradores e usuários.| Permitir que o aplicativo tenha acesso somente leitura aos dados de funcionários.|

7. Defina o  **Estado**  como  **Habilitado** e selecione  **Adicionar escopo**.

8. (Opcional) Para suprimir a solicitação de consentimento dos usuários do seu aplicativo para os escopos que você definiu, é possível  *pré-autorizar*  o aplicativo cliente a acessar sua API Web. Pré-autorize  *apenas*  aplicativos cliente confiáveis, pois os usuários não terão a oportunidade de recusar o consentimento.

   1. Em  **Aplicativos cliente autorizados**, selecione  **Adicionar um aplicativo cliente.**

   2. Insira a  **ID do aplicativo (cliente)**  do aplicativo cliente que deseja pré-autorizar. Por exemplo, aquela de um aplicativo Web que você já registrou.

   3. Em  **Escopos autorizados**, selecione os escopos para os quais deseja suprimir a solicitação de consentimento e escolha  **Adicionar aplicativo**.

   4. Se você seguiu essa etapa opcional, o aplicativo cliente agora é um PCA (aplicativo cliente pré-autorizado), e não será solicitado o consentimento dos usuários ao entrar nele.

#### Tarefa 6 - Adicionar um escopo que requer o consentimento do administrador

Em seguida, adicione outro escopo de exemplo chamado Employees.Write.All, que somente os administradores podem consentir. Os escopos que exigem consentimento do administrador normalmente são usados para fornecer acesso a operações com maior privilégio, muitas vezes, por aplicativos cliente executados como serviços de back-end ou daemons que não conectam um usuário interativamente.

1. Para adicionar o escopo de exemplo Employees.Write.All, siga as etapas acima e especifique esses valores no painel  **Adicionar um escopo** :

    | Campo| Valor de exemplo|
    | :--- | :--- |
    | Nome do escopo| Employees.Write.All|
    | Quem pode consentir| Somente administradores|
    | Nome de exibição de consentimento do administrador| Gravação de acesso aos registros de funcionários|
    | Descrição do consentimento do administrador| Permitir que o aplicativo tenha acesso de gravação a todos os dados de funcionários.|
    | Nome de exibição do consentimento do usuário| Nenhum (deixe em branco)|
    | Descrição de consentimento do usuário| Nenhum (deixe em branco)|

    >**Observação**: Se você tiver adicionado com êxito os dois escopos de exemplo descritos nas seções anteriores, eles aparecerão no painel  **Expor uma API** do registro de aplicativo da API Web, semelhante a esta imagem:

    ![Captura de tela do painel Expor uma API mostrando dois escopos expostos.](./media/portal-03-scopes-list.png)

    Conforme mostrado na imagem, a cadeia de caracteres completa de um escopo é a concatenação do  **URI da ID do Aplicativo**  da sua API Web e o  **Nome do escopo**.

1. Teste a API usando o **URL de ID do aplicativo ** com "/Employees.Read.All" adicionado ao final do URI.

    >**Observação**: Por exemplo, se o URI da ID do aplicativo da API Web for `https://contoso.com/api` e o nome do escopo for Employees.Read.All, o escopo completo será: `https://contoso.com/api/Employees.Read.All`


    >**Observação**: Em seguida você vai configurar o registro de um aplicativo cliente com acesso à API Web e os escopos definidos seguindo as etapas acima.
    Depois que um registro de aplicativo cliente recebe permissão para acessar sua API Web, o cliente pode receber um token de acesso OAuth 2.0 pela plataforma de identidade da Microsoft. Quando o cliente chama a API Web, ele apresenta um token de acesso cuja declaração de escopo (scp) é definida como as permissões que você especificou no registro de aplicativo do cliente.
    É possível expor escopos adicionais posteriormente conforme a necessidade. Considere que sua API Web pode expor vários escopos associados a diversas operações. O recurso pode controlar o acesso a API Web em runtime avaliando declarações de escopo (scp) no token de acesso OAuth 2.0 recebido.


### Exercício 2 –⁠ Gerenciar o registro de aplicativo com uma função personalizada

#### Tarefa 1 - Criar uma função personalizada para permitir acesso para gerenciar registros de aplicativo

Você precisa criar uma nova função personalizada para o gerenciamento de aplicativos. Essa nova função deve ser limitada apenas às permissões específicas necessárias para executar o gerenciamento de credenciais.

1. Entre no  [https://portal.azure.com](https://portal.azure.com) usando uma conta de administrador global.

2. Abra o menu do portal e selecione  **Azure Active Directory**.

3. Na folha Azure Active Directory, em **Gerenciar**, selecione **Funções e administradores**.

4. Na folha Funções e administradores, selecione **+Nova função personalizada** no menu.

    ![Imagem da tela exibindo a folha Funções e administradores com a opção de menu Nova função personalizada realçada](./media/lp3-mod1-new-custom-role.png)

5. Na folha Nova função personalizada, na guia Noções básicas, na caixa de nome, insira **Minha função de aplicativo personalizada**.

6. Examine as opções restantes e selecione **Avançar**.

7. Na guia Permissões, examine as permissões disponíveis.

8. Na caixa **Pesquisar por nome da permissão ou descrição**, insira **credenciais**.

9. Nos resultados, selecione as permissões **Gerenciar** e selecione **Avançar**.

    ```
       microsoft.directory/servicePrincipals/managePasswordSingleSignOnCredentials  -   Manage password single sign-on credentials or service principals.
       microsoft.directory/servicePrincipals/synchronizationCredentials/manage    -   Manage application provisioning secrets and credentials.
    ```

    ![Imagem da tela exibindo a guia Permissões da nova função personalizada com Pesquisar, Gerenciar permissões e Avançar realçados](./media/lp3-mod1-custom-role-permissions.png)

    **Por que escolher esses dois** - Para provisionamento de aplicativo, esses dois itens são as permissões mínimas necessárias para habilitar e impor o logon único para o aplicativo ou entidade de serviço criado e ser capaz de atribuir o aplicativo corporativo a um conjunto de usuários ou grupos.  Outras permissões também podem ser concedidas.  Você pode obter uma lista completa de permissões disponíveis em `https://docs.microsoft.com/azure/active-directory/roles/custom-enterprise-app-permissions`.

10. Examine as alterações e selecione **Criar.**

