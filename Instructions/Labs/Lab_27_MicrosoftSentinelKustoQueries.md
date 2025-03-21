---
lab:
  title: 27 – Consultas Kusto do Microsoft Sentinel para fontes de dados do Microsoft Entra
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Laboratório 27 OPCIONAL — Consultas Kusto do Microsoft Sentinel para fontes de dados do Microsoft Entra

**Observação** — Este laboratório não pode ser feito no ambiente de laboratório de treinamento fornecido no momento.  Estamos deixando a etapa de laboratório aqui para você ter a opção de testá-lo em seu ambiente Traga Sua Própria Assinatura (BYOS).  Leia as etapas para ver o que é possível.  Estamos trabalhando ativamente para atualizar este laboratório para encontrar uma solução alternativa no ambiente de laboratório e o atualizaremos em breve.

### Tipo de logon = logon do recurso do Azure

## Cenário do laboratório

O Microsoft Sentinel é uma solução nativa de nuvem, SIEM e SOAR da Microsoft.  Por meio da conexão de fontes de dados da Microsoft e de soluções de segurança de terceiros, você tem a capacidade de executar tarefas de operações de segurança.  Neste exercício de laboratório, você irá criar um workspace do Microsoft Sentinel com conectores de dados para o Microsoft Entra ID para executar consultas de busca usando Linguagem de Consulta Kusto (KQL). 

#### Tempo estimado: 30 minutos

### Exercício 1 – Configurar o Microsoft Sentinel para consultas Kusto

#### Tarefa 1 – Criar um workspace do Microsoft Sentinel

1. Entre no  [https://portal.azure.com](https://portal.azure.com) como Administrador global.

1. Pesquise pelo **Microsoft Sentinel** e selecione-o. 

1. Selecione **+ Criar** no canto superior esquerdo.

1. No bloco **Adicionar o Microsoft Sentinel a um bloco de workspace**, selecione **+ Criar um novo workspace**.

1. Em **Grupo de recursos**, selecione **Criar novo** e insira **Sentinel-RG**.

1. Nomeie o workspace.  Exemplo – SentinelLogAnalytics.

1. Selecione uma Região próxima de você.

1. Selecione **Examinar + Criar** e **Criar**.

1. Após a conclusão da implantação do workspace do Log Analytics, escolha o botão **Atualizar**. Selecione o workspace e clique em **Adicionar**.  Isso abrirá o Microsoft Sentinel e adicionará o workspace a ele.

1. Se solicitado, selecione **OK** para ativar a avaliação gratuita do Microsoft Sentinel.

#### Tarefa 2 – Adicionar o Microsoft Entra ID como uma fonte de dados

1. No  **Microsoft Sentinel**, navegue pelo menu até **Gerenciamento de conteúdo** e selecione **Hub de Conteúdo**.

1. Use a caixa de pesquisa para procurar o **Entra** na lista de conectores, localize o **Microsoft Entra ID** e marque a caixa de seleção.

1. Um bloco de pré-visualização será aberto à direita.  Selecione **Instalar**.

1. Após a conclusão da instalação, selecione o item de menu **Conectores de dados** no menu Configuração.

    **Observação** – Você deverá ver um conector instalado e ver **Microsoft Entra ID** listado.

1. Selecione **Microsoft Entra ID** e, em seguida, selecione **Abrir página do conector**.

1. Na página do conector, as instruções e as próximas etapas serão fornecidas para o conector de dados. Verifique que uma marca de seleção aparece ao lado de cada um dos **Pré-requisitos** para continuar com a **Configuração**.

1. Em **Configuração**, marque as caixas de **Logs de entrada** e de **Logs de auditoria**. Outras fontes de logs estão disponíveis, mas estão atualmente em **Versão-prévia** e fora do escopo deste curso.

1. Selecione **Aplicar alterações**. 

1. Uma notificação dizendo que as alterações foram aplicadas será exibida. Navegue até o workspace do **Microsoft Sentinel** selecionando o **X** no canto superior direito da página do conector.

1. Selecione **Atualizar** no bloco **Microsoft Sentinel | Conectores de dados** e o número 1 será exibido na contagem **Conectados**.

   **Observação** – pode levar alguns minutos para que o conector de dados do Microsoft Entra seja exibido na contagem ativa. 

#### Tarefa 3 – Executar uma consulta Kusto em uma atividade do usuário

1. No **Microsoft Sentinel**, navegue até **Logs** abaixo do título do menu **Geral**.

1. Feche a janela **Bem-vindo(a) ao Log Analytics**.

1. Uma janela será aberta com consultas de exemplo, selecione **Auditoria** e pesquise por **IDs de usuário**.

1. Selecione **Executar**. 

1. Isso fornecerá uma lista de IDs de usuário no Microsoft Entra ID.  Como acabamos de criar o workspace, talvez você não veja os resultados.  Observe o formato da consulta.
