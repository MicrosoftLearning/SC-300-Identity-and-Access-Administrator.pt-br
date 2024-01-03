---
lab:
  title: 17 – Descoberta de aplicativos do Defender para Nuvem e imposição de restrições
  learning path: '03'
  module: Module 03 - Implement Access Management for Apps
---

# Laboratório 17 – Descoberta de aplicativos do Defender para Nuvem e imposição de restrições

## Cenário do laboratório

Os aplicativos do Microsoft Defender para Nuvem utilizam logs do tráfego de rede para identificar os aplicativos que os usuários estão acessando.Os logs de tráfego de firewalls locais fornecerão um relatório de instantâneos sobre os aplicativos mais comuns e os usuários que estão acessando esses aplicativos.O tráfego de dispositivos gerenciados será alimentado no painel de visão geral da descoberta dos aplicativos do Microsoft Defender para Nuvem.

#### Tempo estimado: 10 minutos

### Exercício 1 – Descoberta de aplicativos do Defender para Nuvem

#### Tarefa 1 – Descoberta de aplicativos no Defender para Nuvem

1. Entre no [https://security.microsoft.com](https://security.microsoft.com)  usando uma conta de administrador global.

1. No menu esquerdo, role até o título chamado **Aplicativos na Nuvem** e clique em **Catálogo de Aplicativos na Nuvem**.

1. No painel **Procurar por categoria**, selecione **Armazenamento em nuvem**.

1. Na lista de aplicativos, observe a **Pontuação de risco** ao lado do nome do aplicativo.  

1. Abra outra guia do navegador e acesse **www.dropbox.com**.

1. Você poderá acessar este site.


#### Tarefa 2 – Restringir aplicativos nos aplicativos do Defender para Nuvem

1. Retorne ao bloco **Aplicativos descobertos** e selecione **Marcar como não sancionado** para o Dropbox.  **Observação**: está localizado ao lado da marca de seleção em círculo.

1. Clique em **Salvar**

1. Esse processo permite que você bloqueie aplicativos que não são sancionados dentro da política da sua empresa, limitando o shadow IT dentro da sua organização.

**Observação**: há um atraso entre a proibição de um aplicativo e o bloqueio do mesmo.

Uma vez que o aplicativo for bloqueado como não sancionado, ele não poderá ser acessado por meio do navegador, navegador privado ou download da loja em um cliente integrado ao MDE (Microsoft Defender para ponto de extremidade) integrado aos aplicativos do Microsoft Defender para Nuvem.



