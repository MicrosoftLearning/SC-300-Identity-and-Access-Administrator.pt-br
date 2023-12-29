---
lab:
  title: 27 - Consultas Kusto do Microsoft Sentinel para fontes de dados do Azure AD
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Laboratório 27 - Consultas Kusto do Microsoft Sentinel para fontes de dados do Azure AD

**Observação** - Este laboratório requer um Azure Pass. Consulte o laboratório 00 para obter instruções.

## Cenário do laboratório

O Microsoft Sentinel é uma solução nativa de nuvem, SIEM e SOAR da Microsoft.  Por meio da conexão de fontes de dados da Microsoft e de soluções de segurança de terceiros, você tem a capacidade de executar tarefas de operações de segurança.  Neste exercício de laboratório, você criará um espaço de trabalho do Microsoft Sentinel com conectores de dados para o Azure AD para executar consultas de busca usando o Linguagem de Consulta Kusto (KQL). 

#### Tempo previsto: 30 minutos

### Exercício 1 - Configurar o Microsoft Sentinel para Consultas Kusto

#### Tarefa 1- Criar um espaço de trabalho do Microsoft Sentinel

1. Entre no  [https://portal.azure.com](https://portal.azure.com) como administrador global.

1. Pesquise pelo **Microsoft Sentinel** e selecione-o. 

1. Selecione **Criar Microsoft Sentinel**.

1. No bloco **Adicionar Microsoft Sentinel a um espaço de trabalho**, selecione **Criar um espaço de trabalho**.

1. Em **Grupo de recursos**, selecione **Criar novo** e insira  **Sentinel-RG**.

1. Dê nome ao espaço de trabalho.  Exemplo - SentinelLogAnalytics.

1. Selecione uma Região próxima de você.

1. Selecione **Examinar + Criar** e **Criar**.

1. Após a conclusão da implantação do espaço de trabalho do Log Analytics, escolha o botão **Atualizar** . Selecione o espaço de trabalho e clique em **Adicionar**.  Isso vai adicionar o espaço de trabalho ao Microsoft Sentinel e abrir o Microsoft Sentinel.

1. Se solicitado, selecione **OK** para ativar a avaliação gratuita do Microsoft Sentinel.

#### Tarefa 2 - Adicionar o Azure AD como fonte de dados

1. Em **Microsoft Sentinel**, acesse o menu **Configuração** e selecione **Conectores de dados**.

1. Na lista de Conectores de dados, localize e selecione o **Azure Active Directory**.

1. Será aberto um bloco de visualização à direita.  Clique em **Abrir página do conector**.

1. Na página do conector, as instruções e as próximas etapas serão fornecidas para o conector de dados. Verifique se uma marca de seleção está ao lado de cada um dos **Pré-requisitos** para continuar com a **Configuração**.

1. Em **Configuração**, marque as caixas de seleção **Logs de entrada** e **Logs de auditoria**. Fontes de log adicionais estão disponíveis, mas estão atualmente em **Visualização** e fora do escopo deste curso.

1. Selecione **Aplicar Alterações**. 

1. Será fornecida uma notificação de que as alterações foram aplicadas com êxito. Acesse o espaço de trabalho **do Microsoft Sentinel ** selecionando o **X** no canto superior direito da página do conector.

1. Selecione **Atualizar** no bloco **Microsoft Sentinel | Conectores de dados** e o número 1 será exibido na contagem **Conectados**.

   **Observação** - O conector de dados do Azure AD pode levar alguns minutos para ser exibido na contagem ativa. 

#### Tarefa 3 - Executar consulta Kusto na atividade do usuário

1. No **Microsoft Sentinel**, navegue até **Logs** no cabeçalho do menu **Geral** .

1. Feche a janela **Bem-vindo ao Log Analytics** .

1. Uma janela será aberta com consultas de exemplo, selecione **Auditoria** e role para localizar **IDs de usuário**.

1. Selecione **Executar**. 

1. Isso fornecerá uma lista de IDs de usuário no Azure AD.  Como acabamos de criar o espaço de trabalho, talvez você não veja os resultados.  Observe o formato da consulta.

1. Em **Gerenciamento de ameaças**, no menu, selecione **Caçada**. 

1. Role para baixo para localizar a consulta **Local de entrada anômalo por conta de usuário e aplicativo de autenticação**.  Essa consulta sobre a entrada no Active Directory do Azure considera todas as entradas de usuário para cada aplicativo do Active Directory do Azure e seleciona a alteração mais anômala no perfil de local de um usuário em um aplicativo individual. A intenção é caçar o comprometimento da conta do usuário, possivelmente por meio de um vetor de aplicativo específico. 

1. Selecione **Visualizar os resultados da consulta** para realizar a consulta.

1. Isso pode não fornecer resultados com o novo espaço de trabalho, mas agora você viu como as consultas podem ser realizadas para coletar informações ou para caçar possíveis ameaças.
