---
lab:
  title: 28 – Monitorar sua postura de segurança gerenciada com a classificação de segurança de identidade
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Lab 28 – Monitorar sua postura de segurança gerenciada com a classificação de segurança de identidade

### Tipo de logon = administração do Microsoft 365

## Cenário do laboratório

O Microsoft Entra Identity Protection fornece detecção e correção automatizadas para riscos baseados em identidade e fornece dados no portal para investigar riscos potenciais. O Microsoft Entra Identity Protection também fornece uma Classificação de Segurança de Identidade para monitorar e melhorar sua postura de segurança de identidade.  Da mesma forma que o Microsoft Defender XDR e o Microsoft Defender para Nuvem, a Classificação de Segurança de Identidade fornece ações de melhoria e recomendações que podem melhorar sua postura de segurança geral para identidade na ID do Microsoft Entra.  Este laboratório vai explorar esta capacidade. 

**Observação** – Como este laboratório está sendo executado em um novo ambiente de locatário criado, você provavelmente receberá uma Classificação de Segurança de Identidade de até 30%.  Leva cerca de 24 horas para que dados viáveis entrem no cálculo para fornecer uma classificação válida.

#### Tempo estimado: 15 minutos

### Exercício 1 – Usando a classificação de segurança de identidade para monitorar e gerenciar a postura de segurança de identidade

#### Tarefa 1 – Analisar a classificação de segurança de identidade e as ações de melhoria

1. Entre no  [https://entra.microsoft.com](https://entra.microsoft.com) como um Administrador global.

2. Abra o menu **Proteção** e selecione **Classificação de Segurança de Identidade**

3. No bloco **Visão geral**, você encontrará a **Classificação de Segurança de Identidade**.

4. Selecione **Classificação de Segurança de Identidade**.  Isso levará você ao painel Classificação de segurança de identidade.

5. Role para baixo para ver as **ações de melhoria**.

**Dica de laboratório** — Ao contrário das ações de melhoria no Microsoft Defender para Nuvem e no Microsoft Defender XDR, essas ações de melhoria são específicas para a identidade.  Isso fornece uma lista mais focada de ações potenciais para o gerenciamento da postura de segurança.  Quaisquer ações de melhoria iniciadas a partir dessa lista também fornecerão um impacto na postura geral de segurança do locatário. 

#### Tarefa 2 – Executar uma ação de melhoria

1. Para melhorar uma área da postura de segurança de identidade, selecione **Habilitar política de risco de entrada do Microsoft Entra ID Protection**.

2. No bloco que é aberto, role para baixo e selecione **Introdução**.

3. Uma nova guia será aberta para **Proteção de Identidade | Política de risco de entrada**.
 **Observação** – por padrão, o botão Introdução abrirá no Portal do Azure. Você pode usar o portal ou voltar para o Centro de Administração do Entra. As duas opções funcionarão.

6. Em Atribuições, escolha o texto **Todos os usuários**.

7. Em Incluir, selecione Todos os usuários.

8. Em Excluir, selecione Usuários e grupos e escolha sua conta de **Administrador MOD**.

  - A Microsoft recomenda que você exclua pelo menos uma conta para impedir que você fique bloqueado.

9. Em Risco de entrada, selecione o texto que diz **Baixo e superior**.

10. Escolha **Médio e superior** e selecione **Concluído**.

10. Na seção **Controles**, escolha o texto que diz **Bloquear acesso**.

11. Selecione **Conceder acesso – Exigir autenticação multifator**.

11. Selecione Concluído.

14. Confirme suas configurações e defina a imposição da política como **Habilitada**.

15. Selecione **Salvar**.
