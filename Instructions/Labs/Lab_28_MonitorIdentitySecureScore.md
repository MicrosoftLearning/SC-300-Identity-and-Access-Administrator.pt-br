---
lab:
  title: 28 - Monitorar e gerenciar sua postura de segurança com a Classificação de Segurança de Identidade
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Laboratório 28 - Monitorar e gerenciar sua postura de segurança com a Classificação de Segurança de Identidade

## Cenário do laboratório

O Azure AD Identity Protection oferece detecção e correção automatizadas para riscos baseados em identidade e fornece dados no portal para investigar riscos potenciais. O Azure AD Identity Protection também fornece uma Classificação de Segurança de Identidade para monitorar e melhorar sua postura de segurança de identidade.  Da mesma forma que o Microsoft 365 Defender e o Microsoft Defender para Nuvem, a Classificação de Segurança de Identidade fornece ações e recomendações de melhoria que podem aprimorar sua postura geral de segurança para identidade no Azure Active Directory.  Este laboratório vai explorar esta capacidade. 

#### Tempo previsto: 15 minutos

### Exercício 1 - Usando a Classificação de Segurança de Identidade para monitorar e gerenciar a postura de segurança de identidade

#### Tarefa 1 - Revisar a Classificação de Segurança de Identidade e as ações de melhoria

1. Entre no  [https://portal.azure.com](https://portal.azure.com) como administrador global.

2. Pesquise e selecione o **Azure AD Identity Protection**.

3. No bloco **Visão geral**, você encontrará a **Classificação de Segurança de Identidade**.

4. Selecione **Classificação de Segurança de Identidade**.  Isso vai levá-lo ao painel da Classificação de Segurança de Identidade.

5. Role para baixo para exibir as **ações de melhoria **.

6. Em contraste com as ações de melhoria no Microsoft Defender para Nuvem e no Microsoft 365 Defender, essas são específicas para a identidade.  Isso fornece uma lista mais focada de ações potenciais para o gerenciamento da postura de segurança.  Todas as ações de melhoria iniciadas a partir dessa lista também fornecerão um impacto na postura geral de segurança do locatário. 

#### Tarefa 2 - Executar uma ação de melhoria

1. Para melhorar uma área da postura de segurança de identidade, selecione **Proteger todos os usuários com uma política de risco de entrada**.

2. No bloco aberto, role para baixo e selecione **Introdução**.

3. Uma nova guia será aberta para **Identity Protection | Política de risco de entrada**.

4. Selecione **Todos os usuários** em **Atribuições**.

5. Selecione **Médio e superior** em **Risco de entrada**.

6. Selecione **Seta** - **Exigir autenticação multifator** em **Controles**.

7. Transforme a **Imposição de política **para **Habilitada** (se isso ainda não tiver sido feito) e selecione **Salvar**.

8. Você criou uma política de risco de entrada que agora deve aumentar sua Classificação de Segurança de Identidade.  Isso vai levar até 24 horas para que tenha efeito em sua Classificação de Segurança de Identidade.

9. Revise outras ações de melhoria e as etapas para criá-las e habilitá-las.
