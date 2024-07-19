---
lab:
  title: 28 – Monitorar sua postura de segurança gerenciada com a classificação de segurança de identidade
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Lab 28 – Monitorar sua postura de segurança gerenciada com a classificação de segurança de identidade

## Cenário do laboratório

O Microsoft Entra Identity Protection fornece detecção e correção automatizadas para riscos baseados em identidade e fornece dados no portal para investigar riscos potenciais. O Microsoft Entra Identity Protection também fornece uma Classificação de Segurança de Identidade para monitorar e melhorar sua postura de segurança de identidade.  Da mesma forma que o Microsoft Defender XDR e o Microsoft Defender para Nuvem, a Classificação de Segurança de Identidade fornece ações de melhoria e recomendações que podem melhorar sua postura de segurança geral para identidade na ID do Microsoft Entra.  Este laboratório vai explorar esta capacidade. 

#### Tempo estimado: 15 minutos

### Exercício 1 – Usando a classificação de segurança de identidade para monitorar e gerenciar a postura de segurança de identidade

#### Tarefa 1 – Analisar a classificação de segurança de identidade e as ações de melhoria

1. Entre no  [https://entra.microsoft.com](https://entra.microsoft.com) como um Administrador global.

2. Abra o menu **Proteção** e selecione **Classificação de Segurança de Identidade**

3. No bloco **Visão geral**, você encontrará a **Classificação de Segurança de Identidade**.

4. Selecione **Classificação de Segurança de Identidade**.  Isso levará você ao painel Classificação de segurança de identidade.

5. Role para baixo para ver as **ações de melhoria**.

6. Ao contrário das ações de melhoria no Microsoft Defender para Nuvem e no Microsoft Defender XDR, essas ações de melhoria são específicas para a identidade.  Isso fornece uma lista mais focada de ações potenciais para o gerenciamento da postura de segurança.  Quaisquer ações de melhoria iniciadas a partir dessa lista também fornecerão um impacto na postura geral de segurança do locatário. 

#### Tarefa 2 – Executar uma ação de melhoria

1. Para melhorar uma área da postura de segurança de identidade, selecione **Proteger todos os usuários com uma política de risco de entrada**.

2. No bloco que é aberto, role para baixo e selecione **Introdução**.

3. Uma nova guia será aberta para **Acesso condicional**.
 **Observação** – por padrão, o botão Introdução abrirá no Portal do Azure. Você pode usar o portal ou voltar para o Centro de Administração do Entra. As duas opções funcionarão.

4. Selecione **+ Nova política**.

5. Dê um nome à sua política. Recomendamos que as organizações criem um padrão significativo para os nomes de suas políticas.

6. Em Atribuições, selecione Usuários ou identidades de carga de trabalho.

7. Em Incluir, selecione Todos os usuários.

8. Em Excluir, selecione Usuários e grupos e escolha as contas que vão continuar podendo usar a autenticação herdada. A Microsoft recomenda que você exclua pelo menos uma conta para impedir que você fique bloqueado.

9. Em Recursos de destino > Aplicativos na nuvem > Incluir, escolha Todos os aplicativos na nuvem.

10. Em Condições > Aplicativos clientes, defina Configurar como Sim.
 - Marque apenas as caixas clientes do Exchange ActiveSync e outros clientes.

11. Selecione Concluído.

12. Em Controles de acesso > Conceder, clique em Bloquear acesso.

13. Escolha Selecionar.

14. Confirme suas configurações e defina Habilitar política com Somente relatório.

15. Selecione Criar para criar e habilitar sua política.
