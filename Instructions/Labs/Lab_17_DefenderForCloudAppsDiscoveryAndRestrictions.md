---
lab:
  title: 17 - Descoberta de aplicativos do Defender para Aplicativos de Nuvem e imposição de restrições
  learning path: '03'
  module: Module 03 - Implement Access Management for Apps
---

# Laboratório 17 - Descoberta de aplicativos do Defender para Aplicativos de Nuvem e imposição de restrições

## Cenário do laboratório

O Microsoft Defender para Aplicativos de Nuvem utiliza logs do tráfego de rede para identificar os aplicativos que os usuários acessam.Os logs de tráfego de firewalls locais fornecerão um relatório de instantâneo sobre os aplicativos mais comuns e os usuários que acessam esses aplicativos.O tráfego de dispositivos gerenciados será alimentado no painel de visão geral de descoberta do Microsoft Defender para Aplicativos de Nuvem

#### Tempo previsto: 10 minutos

### Exercício 1 - Descoberta do Defender para Aplicativos de Nuvem

#### Tarefa 1 - Descoberta de aplicativos no Defender para Aplicativos de Nuvem

1. Entre no [https://security.microsoft.com](https://security.microsoft.com) usando uma conta de administrador global.

1. No menu esquerdo, role até o título chamado **Aplicativos de Nuvem** e clique em **Catálogo de Aplicativos de Nuvem**.

1. No painel **Procurar por categoria** , selecione **Armazenamento em nuvem**.

1. Na lista de aplicativos, observe a **Classificação de risco** ao lado do nome do aplicativo.  

1. Abra outra guia do navegador e navegue até **Dropbox.com**.

1. Você poderá acessar este site.


#### Tarefa 2 - Restringir aplicativos no Defender para Aplicativos de Nuvem

1. Retorne ao bloco **Aplicativos descobertos** e selecione **Marcar como Não Sancionado** para o Dropbox.  **Observação**: isto está localizado próximo à marca de seleção circulada.

1. Clique em **Salvar**

1. Esse processo permite que você bloqueie aplicativos que não são sancionados dentro da política da sua empresa, limitando o Shadow IT dentro da sua organização.

**Observação**: Há um atraso entre a não sanção de um aplicativo e o bloqueio desse aplicativo.

Depois que o aplicativo for bloqueado como não sancionado, não poderá ser acessado por meio do navegador, navegador privado ou download da loja em um cliente integrado ao MDE (Microsoft Defender para Ponto de Extremidade) integrado ao Microsoft Defender para Aplicativos de Nuvem.



