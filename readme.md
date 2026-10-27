# Aliança Francesa Rio · Sistema de Cadastro e Sorteio de Ingressos

Sistema leve, gratuito e hospedado via **GitHub Pages** integrado a uma **Google Planilha** (via **Google Apps Script**), desenvolvido para gerenciar inscrições de participantes em eventos presenciais e realizar sorteios ao vivo através de uma roleta interativa.

---

## 🚀 Funcionalidades

- **Formulário do Participante (`?evento=slug`)**: Coleta nome completo, e-mail, status de aluno, interesse em aprender francês, autorização de newsletter e canal de captação (Instagram, WhatsApp, TikTok, etc.). Bloqueia inscrições caso o evento tenha sido encerrado pela equipe.
- **Painel Administrativo (`?admin`)**: Protegido por senha para gerenciar eventos, visualizar a lista de participantes (com opção de mascarar e-mails por privacidade), gerar/baixar QR Codes em formato SVG, alternar status de encerramento de inscrições e operar a **Roleta de Sorteios** ao vivo.
- **Roleta Dinâmica**: Permite filtrar participantes elegíveis (todos, apenas alunos, não alunos, não alunos interessados em francês) e realiza sorteios animados sem expor dados sensíveis de contato na tela de projeção.
- **Banco de Dados Automatizado**: Cada evento cria automaticamente uma aba dedicada na Google Planilha vinculada, formatada profissionalmente com colunas ajustadas, centralização e estilo visual institucional.

---

## 🛠️ Guia de Instalação e Configuração

### 1. Configurando a Google Planilha (Backend)
1. Crie uma nova **Google Planilha** vazia no seu Google Drive.
2. No menu superior, clique em **Extensões** > **Apps Script**.
3. Apague qualquer código existente no editor e cole o script completo do arquivo `Code.gs` fornecido no projeto.
4. Altere a senha de administrador na constante do código:
   ```javascript
   const CHAVE_ADMIN = 'SUA_SENHA_SECRETA';
   ```
5. Clique no ícone de disquete (**Salvar**).
6. No canto superior direito, clique em **Implantar** > **Nova implantação**.
   - **Tipo de item:** Aplicativo da Web (*Web app*).
   - **Executar como:** Eu (sua conta).
   - **Quem pode acessar:** **Qualquer pessoa** (*Anyone*). *(Atenção: essa permissão pública é obrigatória para o site funcionar).*
7. Conceda as permissões de conta solicitadas pelo Google e copie a **URL do Executável** gerada (terminada em `/exec`).

### 2. Configurando o Front-end (GitHub Pages)
1. Abra o arquivo **`index.html`** do projeto e cole a URL do Apps Script na constante do topo:
   ```javascript
   const API = 'SUA_URL_DO_APPS_SCRIPT_TERMINADA_EM_EXEC';
   ```
2. Crie um repositório público no [GitHub](https://github.com) (ex: `sorteio-af`).
3. Faça o upload do arquivo **`index.html`** renomeado exatamente para `index.html` na raiz do repositório.
4. Vá em **Settings** > **Pages**.
   - Em *Build and deployment*, selecione **Deploy from a branch**.
   - Escolha a branch **main** (ou master) e a pasta **/ (root)**, depois clique em **Save**.
5. Aguarde cerca de 1 a 2 minutos. O endereço público do seu sistema aparecerá no topo da página de configurações no formato: `https://seu-usuario.github.io/sorteio-af/`

---

## 📋 Como Utilizar no Dia do Evento

1. **Acessar o Painel da Equipe**: Abra o endereço do seu site adicionando `?admin` ao final da URL (ex: `https://seu-usuario.github.io/sorteio-af/?admin`).
2. **Fazer Login**: Insira a senha cadastrada no Apps Script.
3. **Criar um Evento**: Clique no botão *Criar evento*, digite o nome oficial (ex: *Festival de Cinema Francês*). O sistema gerará o link e o slug automaticamente.
4. **Gerar o QR Code**: Navegue até a aba **QR Code** do evento criado e faça o download do arquivo SVG ou copie o link para divulgar.
5. **Realizar o Sorteio**: No dia, abra a aba **Roleta** no painel da equipe, filtre o público desejado e clique em *Girar a roleta* para projetar o ganhador na tela com total segurança e elegância.
6. **Encerrar o Evento**: Assim que o evento terminar, clique no botão *Encerrar evento* no painel para desativar instantaneamente o QR Code e bloquear novos cadastros.