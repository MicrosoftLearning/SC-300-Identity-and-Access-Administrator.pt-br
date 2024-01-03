---
lab:
  title: 04 – Definir configurações de colaboração externa
  learning path: '01'
  module: Module 01 - Implement an identity management solution
---

# Laboratório 04: Definir configurações de colaboração externa

## Cenário do laboratório

Você deve habilitar as configurações de colaboração externa para sua organização para acesso de convidados aprovados.

#### Tempo estimado: 5 minutos

### Exercício 1 – Permitir que usuários convidados sejam chamados para sua organização

#### Tarefa 1 – Permitir que usuários convidados realizem a inscrição por autoatendimento

1. Entre em  [https://entra.microsoft.com](https://entra.microsoft.com)  como um administrador de locatários.
2. Selecione  **Identidade** e, em seguida, selecione **Usuários**.
3. Abra o item de menu **Todos os usuários** e selecione **Configurações de usuário**.
4. Clique em **Gerenciar configurações de colaboração de usuário externo**.
5. Verifique se **SIM** está marcado para a configuração **Habilitar inscrição de autoatendimento de convidado por meio de fluxos de usuário**.
6. Selecione **Salvar** na parte superior da tela.

#### Tarefa 2 – Definir configurações de colaboração externa

1. Entre em  [https://entra.microsoft.com](https://entra.microsoft.com)  como um administrador de locatários.
2. Selecione **Identidade**.
3. Selecione  **Identidades externas** e, em seguida, selecione **Todos os provedores de identidade**.
4. Selecione o link de notificação **Senha de uso único por email** que você vê próximo à parte superior da tela.

    **Observação** – A senha de uso único é uma maneira segura de convidar um usuário para ingressar em sua organização.
    
5. Verifique se a opção **Sim** está selecionada.
6. Se necessário, selecione **Salvar**.
7. Caso contrário, selecione `Home > Contoso Marketing >`**Identidades Externas** para retornar à tela anterior.
8. Selecione **Configurações de colaboração externa** na esquerda

9. Em  **Acesso de usuário convidado**, examine os níveis de acesso que estão disponíveis e selecione **Acesso do usuário convidado é restrito a propriedades e associações dos próprios objetos de diretório (mais restritivo)**.

    **OBSERVAÇÃO**
    - Os usuários convidados têm o mesmo acesso que os membros (mais inclusivo): essa opção fornece aos convidados o mesmo acesso aos recursos do Microsoft Entra e aos dados de diretório que os usuários membros.
    - Os usuários convidados têm acesso limitado a propriedades e associações de objetos do directory (padrão) : essa configuração bloqueia convidados de determinadas tarefas de diretório, como a enumeração de usuários, grupos ou outros recursos de diretório. Os convidados podem ver a associação de todos os grupos não ocultos.
    - O acesso do usuário convidado é restrito a propriedades e associações de objetos próprios do diretório (mais restritivo) : com essa configuração, os convidados podem acessar somente os próprios perfis. Os convidados não têm permissão para ver os perfis, grupos ou associações de grupo dos outros usuários.

    ![Imagem da tela exibindo opções de restrição do acesso do usuário convidado.](./media/lp1-mod3-guest-user-access-restrictions.png)

10. Em  **Configurações de convite de convidado**, selecione **Os usuários membros e os usuários atribuídos a funções de administrador específicas podem convidar usuários convidados, incluindo os convidados com permissões de membro**!

    **OBSERVAÇÃO**
    - Todas as pessoas na organização, incluindo os convidados e os que não são administradores, podem convidar usuários convidados (opção mais inclusiva): para permitir que convidados na organização chamem outros convidados, incluindo aqueles que não são membros de uma organização, selecione esse botão de opção.
    - Os usuários membros e os usuários atribuídos a funções de administrador específicas podem convidar usuários convidados, incluindo os convidados com permissões de membro: para permitir que usuários membros e usuários com funções de administrador específicas chamem convidados, selecione esse botão de opção.
    - Somente os usuários atribuídos a funções de administrador específicas podem convidar usuários convidados: para permitir que somente os usuários com funções de administrador chamem convidados, selecione esse botão de opção. As funções de administrador incluem Administrador Global, Administrador de Usuárioe Emissor do Convite ao Convidado.
    - Ninguém na organização, incluindo os administradores, pode convidar usuários convidados (opção mais restritiva) : para negar que todos na organização chamem convidados, selecione esse botão de opção.
    - Se a opção Membros podem convidar estiver definida como Não e os Administradores e usuários na função de emissor do convite estiverem definidos como Sim, os usuários na função Emissor do convite ainda poderão convidar convidados.

    ![Imagem da tela exibindo as configurações de convite de convidado com a opção Convidados podem convidar definida como Não e realçada](./media/lp1-mod3-guest-user-invite-settings.png)

11. Em  **Restrições de colaboração**, examine as opções disponíveis e aceite as configurações padrão.

    **IMPORTANTE**
    - Você pode criar uma lista de permissões ou uma lista de negações. Você não pode configurar os dois tipos de listas. Por padrão, qualquer domínio que ão esteja na lista de permissão ou na lista de negação, e vice-versa.
    - Você pode criar apenas uma política por organização. Você pode atualizar a política para incluir mais domínios ou você pode excluir a política para criar uma nova.
    - O número de domínios que você pode adicionar a uma lista de permissões ou lista de negações é limitado apenas pelo tamanho da política. O tamanho máximo de toda a política é 25 KB (25.000 caracteres), que inclui a lista de permissões ou a lista de negações e quaisquer outros parâmetros configurados para outros recursos.
    - Esta lista funciona independentemente das listas de permissão/bloqueio do OneDrive for Business e SharePoint Online. Se você quiser restringir o compartilhamento de arquivos no SharePoint Online, será necessário configurar uma lista de permissão ou negação para o One Drive for Business e para o SharePoint Online.
    - A lista não se aplica a usuários externos que já resgataram o convite. A lista será aplicada depois que for configurada. Se um convite do usuário estiver em um estado pendente e você definir uma política que bloqueia seu domínio, a tentativa do usuário para resgatar o convite falhará.

12. Após terminar, **salve** suas alterações.
