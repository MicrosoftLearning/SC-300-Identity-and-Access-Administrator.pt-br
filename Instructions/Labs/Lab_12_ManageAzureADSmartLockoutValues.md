---
lab:
  title: 12- Gerenciar valores de bloqueio inteligente do Azure AD
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# Laboratório 12 - Gerenciar valores de bloqueio inteligente do Azure AD

## Cenário do laboratório

Você deve definir as configurações adicionais de proteção por senha para sua organização.

#### Tempo previsto: 5 minutos

### Exercício 1 - Gerenciar valores de bloqueio inteligente do Azure AD

#### Tarefa - Adicionar bloqueios inteligentes

Com base em seus requisitos organizacionais, você pode personalizar os valores do bloqueio inteligente do Azure AD. A personalização das configurações de bloqueio inteligente, com valores específicos de sua organização, requer o Azure AD Premium P1 ou superior licenças para seus usuários.

1. Navegue até o [https://portal.azure.com](https://portal.azure.com) e entre usando uma conta de administrador global para o diretório.

2. Abra o menu do portal e selecione  **Azure Active Directory**.

3. Na página do Azure Active Directory, em **Gerenciar**, selecione **Segurança**.

4. Na página Segurança, na navegação à esquerda, selecione **Métodos de autenticação**.

5. Na navegação à esquerda, selecione **Proteção por senha**.

    ![Imagem da tela exibindo a página Métodos de autenticação e as seleções realçadas para navegar até a Autenticação por senha](./media/lp2-mod3-browse-to-password-protection.png)

6. Nas configurações da Proteção por senha, na caixa **Duração do bloqueio em segundos**, defina o valor como **120**.

7. Ao lado de **Modo**, selecione **Imposto**.

8. Salve suas alterações.

    **OBSERVAÇÃO** - Quando o limite para bloqueio inteligente for acionado, você receberá a seguinte mensagem enquanto a conta estiver bloqueada:
    - Sua conta está temporariamente bloqueada para impedir o uso não autorizado. Tente novamente mais tarde e, se ainda tiver problemas, entre em contato com o administrador.

9. Isso pode ser testado escolhendo um usuário em seu locatário do Azure AD. Acesse um navegador particular até <login.microsoftonline.com> e insira uma senha incorreta até que a conta receba a notificação de que está bloqueada.
