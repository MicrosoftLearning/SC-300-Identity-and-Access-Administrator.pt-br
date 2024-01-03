---
lab:
  title: 28 – Monitorar sua postura de segurança gerenciada com a classificação de segurança de identidade
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Lab 28 – Monitorar sua postura de segurança gerenciada com a classificação de segurança de identidade

## Cenário do laboratório

O Microsoft Entra Identity Protection fornece detecção e correção automatizadas para riscos baseados em identidade e fornece dados no portal para investigar riscos potenciais. O Microsoft Entra Identity Protection também fornece uma classificação de segurança de identidade para monitorar e melhorar sua postura de segurança de identidade.  Da mesma forma que o Microsoft 365 Defender e o Microsoft Defender para Nuvem, a classificação de segurança de identidade fornece ações e recomendações de melhoria que podem aprimorar sua postura geral de segurança para identidades no Microsoft Entra ID.  Este laboratório vai explorar esta capacidade. 

#### Tempo estimado: 15 minutos

### Exercício 1 – Usando a classificação de segurança de identidade para monitorar e gerenciar a postura de segurança de identidade

#### Tarefa 1 – Analisar a classificação de segurança de identidade e as ações de melhoria

1. Entre no  [https://entra.microsoft.com](https://entra.microsoft.com) como um Administrador global.

2. Abra o menu **Proteção** e selecione **Classificação de Segurança de Identidade**

3. No bloco **Visão geral**, você encontrará a **Classificação de Segurança de Identidade**.

4. Selecione **Classificação de Segurança de Identidade**.  Isso levará você ao painel Classificação de segurança de identidade.

5. Role para baixo para ver as **ações de melhoria**.

6. Em contraste com as ações de melhoria no Microsoft Defender para Nuvem e no Microsoft 365 Defender, essas ações de melhoria são específicas para a identidade.  Isso fornece uma lista mais focada de ações potenciais para o gerenciamento da postura de segurança.  Quaisquer ações de melhoria iniciadas a partir dessa lista também fornecerão um impacto na postura geral de segurança do locatário. 

#### Tarefa 2 – Executar uma ação de melhoria

1. Para melhorar uma área da postura de segurança de identidade, selecione **Proteger todos os usuários com uma política de risco de entrada**.

2. No bloco que é aberto, role para baixo e selecione **Introdução**.

3. Uma nova guia será aberta para **Proteção de Identidade | Política de risco de entrada**.

4. Selecione **Todos os usuários** em **Atribuições**.

5. Selecione **Médio e superior** em **Risco de entrada**.

6. Selecione **Permitir** - **Exigir autenticação multifator**, em **Controles**.

7. Transforme a **imposição de política** para **Habilitada** (se ainda não tiver sido feita) e selecione **Salvar**.

8. Você criou uma política de risco de entrada que agora deve aumentar sua classificação de segurança de identidade.  Isso levará até 24 horas para entrar em vigor na sua classificação de segurança de identidade.

9. Revise outras ações de melhoria e as etapas para criá-las e habilitá-las.
