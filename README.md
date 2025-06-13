# Páginas do Captive Portal para pfSense

Este repositório contém páginas HTML personalizadas para o Captive Portal do pfSense, projetadas para oferecer uma experiência de login amigável e com um estilo visual consistente. As páginas incluem uma interface de login, uma página de erro e uma página de logout, todas adaptadas para funcionar com as variáveis e configurações do pfSense.

## Visão Geral das Páginas

### 1. Página de Login (`captive_portal_login.html`)
- **Propósito**: Permite que os usuários se autentiquem e acessem a rede.
- **Design Inicial**: 
  - Design minimalista com uma imagem de fundo (`captiveportal-background.jpg`) e um logotipo (`captiveportal-logo.png`).
  - Campos para "Usuário" e "Senha" com fundo cinza (`#4b5563`) e cantos arredondados.
  - Botão "Conectar" em vermelho (`#dc2626`).
- **Principais Alterações**:
  - Removido o texto "Wi-Fi" e "ASUS Free WiFi", deixando apenas o logotipo.
  - Aumentado o tamanho do logotipo para `max-width: 150px` (tamanho padrão).
  - Suavizada a cor dos campos para cinza (`#4b5563`) para melhor contraste com fundo preto e logotipo laranja/cinza.
  - Adicionado espaçamento entre "Senha" e "Conectar" (`1rem`).
  - Traduzidos os campos para português: "Enter Account" → "Usuário", "Enter Password" → "Senha", "Connect" → "Conectar".
  - Ajustado para redirecionar para `https://www.google.com` após login bem-sucedido, em vez de exibir "Seja bem-vindo" (devido ao comportamento de redirecionamento do pfSense).
- **Notas**: O redirecionamento para o Google depende da configuração de **Redirecionamento Após Login** no pfSense. Certifique-se de que `https://www.google.com` esteja em **Hostnames Permitidos**.

### 2. Página de Erro (`captive_portal_error.html`)
- **Propósito**: Exibe uma mensagem de erro quando a autenticação falha.
- **Design Inicial**: 
  - Imagem de fundo (`captiveportal-background.jpg`) com logotipo centralizado (`captiveportal-logo.png`).
  - Área de mensagem de erro com texto branco.
- **Principais Alterações**:
  - Definida uma mensagem fixa: "Credenciais inválidas, verifique usuário e senha e tente novamente" em duas linhas.
  - Adicionado um botão "Voltar para Login" em vermelho (`#dc2626`) para retornar à página de login.
- **Notas**: O botão utiliza `#PORTAL_ACTION#` e `#PORTAL_REDIRURL#` para redirecionamento. Verifique a configuração do pfSense para navegação correta.

### 3. Página de Logout (`captive_portal_logout.html`)
- **Propósito**: Confirma a desconexão do usuário da rede.
- **Design Inicial**: 
  - Imagem de fundo (`captiveportal-background.jpg`) com logotipo centralizado (`captiveportal-logo.png`).
  - Mensagem "Você foi desconectado com sucesso" com botão "Sair" em vermelho (`#dc2626`).
- **Principais Alterações**:
  - Sem alterações significativas; mantida como alvo para logout manual ou redirecionamento (se configurado).
- **Notas**: Utilizada como página padrão de logout quando o usuário escolhe sair manualmente.

## Instalação e Configuração

### Pré-requisitos
- pfSense instalado e configurado com uma zona de Captive Portal.
- Imagem de fundo (`captiveportal-background.jpg`) e logotipo (criar ou adicionar) (`captiveportal-logo.png`) enviados para o mesmo diretório (ex.: via **System > File Manager**).
- Certifique-se de que as imagens estejam acessíveis e listadas em **Hostnames Permitidos** ou **Endereços IP Permitidos** se usar URLs externas.

### Passos
1. **Acesse o pfSense**:
   - Navegue até **Serviços > Captive Portal** e edite a zona desejada.
2. **Ative as Páginas Personalizadas**:
   - **Página de Login**: Marque **Usar página personalizada de Captive Portal** e cole `captive_portal_login.html` em **Conteúdo da Página HTML**.
   - **Página de Erro**: Marque **Usar página personalizada de erro de Captive Portal** e cole `captive_portal_error.html` em **Conteúdo da Página de Erro**.
   - **Página de Logout**: Marque **Usar página personalizada de logout de Captive Portal** e cole `captive_portal_logout.html` em **Conteúdo da Página de Logout**.
3. **Configure a Imagem de Fundo**:
   - Substitua `captiveportal-background.jpg` no CSS (linha 14 de cada arquivo) pelo nome ou caminho correto do arquivo (ex.: `/captiveportal/sua-imagem.jpg`).
   - Envie a imagem para o mesmo diretório do logotipo ou hospede externamente e adicione o URL em **Hostnames Permitidos**.
4. **Defina o Redirecionamento (Página de Login)**:
   - Nas configurações da zona do Captive Portal, defina **Redirecionamento Após Login** como `https://www.google.com` para alinhar com o valor de `redirurl`.
   - Certifique-se de que `https://www.google.com` esteja em **Hostnames Permitidos**.
5. **Salve e Teste**:
   - Clique em **Salvar** e **Aplicar Alterações**.
   - Teste login, cenários de erro e logout para verificar a funcionalidade.

## Notas Adicionais
- **Logotipo**: O logotipo deve ser otimizado para largura de `150px` e projetado com cores laranja e cinza para corresponder ao estilo descrito.
- **Responsividade**: O design se ajusta para telas menores que 480px (logotipo para `125px`, campos para `90% de largura`).
- **HTTPS**: Configure HTTPS com um certificado (ex.: via Let’s Encrypt) para evitar avisos de segurança.
- **Personalização**: Ajuste cores, espaçamentos ou mensagens editando o CSS e o HTML conforme necessário.

## Contribuição
Sinta-se à vontade para fazer fork deste repositório, realizar melhorias e enviar pull requests. Relate problemas ou sugestões pela aba Issues.

## Licença
Este projeto está licenciado sob a Licença MIT - veja o arquivo [LICENSE](LICENSE) para detalhes.
