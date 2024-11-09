---
lab:
  title: 16 – Usar o Azure Key Vault para Identidades gerenciadas
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# Laboratório 16 – Usar o Azure Key Vault para Identidades gerenciadas

**Observação** – Este laboratório requer um Azure Pass. Consulte o laboratório 00 para obter instruções.

## Cenário do laboratório

Ao usar as identidades gerenciadas nos recursos do Azure, seu código pode obter tokens de acesso para se autenticar nos recursos que dão suporte à autenticação do Microsoft Entra.No entanto, nem todos os serviços do Azure dão suporte à autenticação do Microsoft Entra. Para usar identidades gerenciadas em recursos do Azure com esses serviços, armazene as credenciais de serviço no Azure Key Vault e use a identidade gerenciada para acessar o Key Vault e recuperar as credenciais.

#### Tempo estimado: 20 minutos

### Exercício 1 - Usar o Azure Key Vault para gerenciar identidades de Máquina Virtual

#### Tarefa 1 – Criar uma máquina virtual do Windows

1. Navegue para o [https://portal.azure.com](https://portal.azure.com)

1. Selecione **+ Criar um recurso**.

1. Digite **Windows 11** na barra de pesquisa Pesquisar no Marketplace.

1. Selecione **Windows 11** e, na lista suspensa do plano, escolha **Windows 11 Enterprise, versão 21H2**. Em seguida, escolha **Criar**.

1. Você precisará criar um nome de usuário administrador e uma senha para a VM na guia Básico.

1. Na guia **Gerenciamento**, marque a caixa **Habilitar identidade gerenciada atribuída ao sistema**.

1. Percorra o restante da experiência de criação de uma máquina virtual. 

1. Selecione Criar.

#### Tarefa 2 – Criar um Key Vault

1. Entre no  [https://portal.azure.com]( https://portal.azure.com) usando uma Conta de administrador global.

1. Na parte superior da barra de navegação esquerda, selecione Criar um recurso

1. Na caixa Pesquisar no Marketplace, digite **Key Vault**.  

1. Selecione **Key Vault** nos resultados.

1. Selecione **Criar**.

1. Preencha todas as informações necessárias, conforme mostrado abaixo. Certifique-se de escolher a assinatura que você está usando para este laboratório.
    **Observação** O nome do Cofre de chaves precisa ser exclusivo. Procure uma marca de seleção verde à direita do campo.

 - **Grupo de recursos** – sc300KeyVaultrg
 - **Nome do cofre de chaves** - *anyuniquevalue*
 - Na página **Configuração de acesso**, selecione o botão de opção **Política de Acesso do Cofre**.
1. Selecione **Examinar + criar**.

1. Selecione **Criar**.


#### Tarefa 3 – Criar um segredo

1. Navegue até o Key Vault recém-criado.

1. Selecione **Segredos**.

1. Selecione **+ Gerar/importar**.

1. Na tela Criar um segredo, em Opções de upload, deixe **Manual** selecionado.

1. Insira um nome e um valor para o segredo.  O valor pode ser qualquer coisa que você desejar. 

1. Deixe a data de ativação e a data de validade em branco e deixe Habilitado como Sim. 

1. Selecione **Criar** para criar o segredo.

#### Tarefa 4 – Permitir acesso ao Cofre de chaves

1. Navegue até o Key Vault recém-criado

1. Selecione **Política de Acesso** no menu no lado esquerdo.

1. Selecione **+ Criar**.

1. Na seção Adicionar política de acesso em Configurar com base no modelo (opcional), escolha Gerenciamento de Segredo no menu suspenso.

1. Em **Selecionar entidade de segurança**, escolha **Nenhuma selecionada** para abrir a lista de entidades a serem selecionadas. No campo de pesquisa, insira o nome da VM criada na tarefa 2.  Selecione a VM na lista de resultados e escolha Selecionar.

1. Selecione **Adicionar**.

1. Selecione **Salvar**.

#### Tarefa 5 – Acessar dados usando o segredo do Cofre de Chaves com o PowerShell

1. Na máquina virtual de laboratório, abra o PowerShell.  

1. No PowerShell, invoque a solicitação Web no locatário para obter o token para o host local na porta específica para a máquina virtual.  

    ```
    $Response = Invoke-RestMethod -Uri 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fvault.azure.net' -Method GET -Headers @{Metadata="true"}
    ```

1. Em seguida, extraia o token de acesso da resposta.  

    ```
    $KeyVaultToken = $Response.access_token
    ```

1. Use o comando de Invoke-WebRequest do PowerShell para recuperar o segredo que você criou anteriormente no Cofre de Chaves, passando o token de acesso no cabeçalho de Autorização.  Você precisará da URL de seu Key Vault, que está na seção Essentials da página Visão geral do Key Vault.  Lembrete – O URI do Cofre de Chaves está na guia Visão geral.

    ```
    Invoke-RestMethod -Uri https://<your-key-vault-URI>/secrets/<secret-name>?api-version=2016-10-01 -Method GET -Headers @{Authorization="Bearer $KeyVaultToken"}
    ```
1. Você deve receber uma resposta semelhante à mostrada a seguir: 
    ```
    'My Secret' https://mi-lab-vault.vault.azure.net/secrets/mi-test/50644e90b13249b584c44b9f712f2e51 @{enabled=True; created=16…
    ```
1. Esse segredo pode ser usado para autenticar serviços que exigem um nome e senha.
