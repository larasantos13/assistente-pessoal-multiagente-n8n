# Assistente Pessoal Completo (Atualizado)

Este projeto utiliza um **workflow do n8n** chamado **“Assistente Pessoal Completo (Atualizado)”**.  
Ele define um **orquestrador multiagente** que integra vários serviços (**Telegram, Gmail, Google Calendar, Google Contacts, Tavily, OpenAI, etc.**) para funcionar como um **assistente pessoal automatizado**.

---

## 📌 Estrutura do Workflow

### 1. Entrada e Orquestração
- **Telegram (Gatilho)** → ponto de entrada. Sempre que você manda uma mensagem (texto ou áudio) no Telegram, o fluxo é disparado.  
- **Switch** → identifica se a mensagem recebida é **voz** ou **texto**.  
  - Se for **voz** → baixa o arquivo (**Baixar Arquivo de Voz**) e envia para o **Áudio para Texto (OpenAI)**.  
  - Se for **texto** → vai direto para o nó **Set 'Text'**.  
- O texto processado é entregue ao **Assistente Pessoal Completo**, que é o **agente orquestrador**.

---

### 2. Agente Orquestrador
- O **Assistente Pessoal Completo** não resolve as tarefas sozinho: ele **decide para qual agente especializado encaminhar**.  
- Mantém **memória de conversas (Simple Memory)** para contexto.  
- Pode chamar ferramentas como:  
  - 📧 **AgenteDeEmail**  
  - 📅 **AgenteDeCalendario**  
  - 👥 **AgenteDeContatos**  
  - ✍️ **CriadorDeConteudo**  
  - 🌐 **Tavily** (pesquisa na web)  
  - 🧮 **Calculadora**

---

### 3. Agentes Específicos

#### 🔹 AgenteDeEmail
Integra com **Gmail**:  
- Enviar email (`enviarEmail`)  
- Responder (`responderEmail`)  
- Criar rascunho (`criarEsboco`)  
- Buscar emails (`buscarEmails`)  
- Buscar etiquetas (`buscarEtiquetas`)  
- Marcar como não lido (`marcarComoNaoVisualizado`)  
- Adicionar etiqueta (`adicionarEtiqueta`)  

👉 Todos os emails são formatados em **HTML profissional**, assinados como **“Salu Sparo”**.

---

#### 🔹 AgenteDeCalendario
Integra com **Google Calendar**:  
- Criar evento simples ou com participante (`Criar Evento`, `Criar Evento Com Participante`)  
- Buscar eventos (`Buscar Eventos`)  
- Atualizar eventos (`Atualizar Evento`)  
- Apagar eventos (`Apagar Evento`)  

👉 Sempre retorna o **link do evento criado/alterado**.

---

#### 🔹 AgenteDeContatos
Integra com **Google Contacts**:  
- Buscar contato (`Buscar Contatos`)  
- Listar todos os contatos (`Buscar Todos os Contatos do Google`)  
- Atualizar contato (`Atualizar Contato`)  
- Criar contato (`Criar Contato`)  

👉 Exige sempre o **Contact ID** antes de atualizar.

---

#### 🔹 CriadorDeConteudo
Integra **OpenAI + Tavily** para criar posts de blog.  
- Sempre escreve em **HTML estruturado** (`<h1>, <p>, <ul>`).  
- Links do Tavily viram **hiperlinks clicáveis**.  
- Otimiza para **SEO** e fluidez de leitura.  

---

### 4. Conexões entre Nós
- Todos os agentes (Email, Calendário, Contatos, Conteúdo) são conectados ao **Assistente Pessoal Completo**.  
- O orquestrador centraliza as decisões e envia a resposta ao usuário pelo **Telegram (Resposta)**.

---

### 5. Regras do Orquestrador
- Nunca cria conteúdo sozinho: **sempre chama o agente certo**.  
- Para enviar emails ou criar eventos com participantes, é necessário **buscar o contato primeiro**.  
- Inclui um nó de **“Think” (reflexão)** para validar se a decisão está correta antes de agir.  

---

## ✅ Resumindo
Esse workflow implementa um **super assistente pessoal integrado ao Telegram**, que:  

✔️ Entende texto ou voz.  
✔️ Pode enviar e responder emails pelo **Gmail**.  
✔️ Gerencia a agenda no **Google Calendar**.  
✔️ Busca, cria e atualiza contatos no **Google Contacts**.  
✔️ Cria posts de blog usando **OpenAI + Tavily**.  
✔️ Mantém **memória de conversas**.  
✔️ Centraliza tudo num **Agente Orquestrador inteligente**.  

---

## 📊 Visualização
![Fluxograma do Assistente](assistente_pessoal_fluxo.png)
