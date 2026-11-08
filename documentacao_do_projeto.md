# 🍲 AproveitAI — Assistente Culinário Inteligente

O **AproveitAI** é um agente conversacional desenvolvido em Python para a atividade *"Meu Primeiro Agente de IA com LLM"*. Seu objetivo é ajudar usuários a prepararem receitas com os ingredientes que já têm em casa, combater o desperdício alimentar (aproveitando talos, cascas e sobras) e sugerir compras complementares dentro do orçamento disponível.

## 🚀 Tecnologias Utilizadas

- **Python 3.10+**
- **Streamlit** (Interface web interativa)
- **LangChain** (`langchain-core` e `langchain-google-genai` para orquestração e memória de contexto)
- **Google Gemini API** (Modelo `gemini-3.5-flash-lite`)

## 📦 Instalação

1. Clone este repositório ou acesse a pasta do projeto no terminal:
   ```bash
   cd caminho/para/o/projeto
   ```

2. Instale as dependências necessárias:
   ```bash
   pip install streamlit langchain-core langchain-google-genai
   ```
   *(Ou utilize `pip install -r requirements.txt` caso o arquivo esteja presente na pasta).*

## 🔑 Configuração da Chave de API

1. Acesse o [Google AI Studio](https://aistudio.google.com/) e gere uma **API Key** gratuita.
2. Você pode informar a chave de duas formas:
   - **Pela interface web:** Cole a chave diretamente no menu lateral esquerdo ao abrir a aplicação.
   - **Por variável de ambiente (opcional):**
     ```powershell
     $env:GOOGLE_API_KEY="SUA_CHAVE_AQUI"
     ```

## ▶️ Como Executar

No terminal, dentro da pasta do projeto, execute:

```bash
streamlit run app.py
```

O aplicativo abrirá automaticamente no navegador em `http://localhost:8501`.

### 🌐 Compartilhamento em Rede Externa (Opcional via ngrok)

Para gerar um link público temporário para testes em equipe:

1. Inicie o Streamlit com suporte a túnel:
   ```powershell
   streamlit run app.py --server.enableCORS=false --server.enableXsrfProtection=false
   ```
2. Em outro terminal, inicie o ngrok na porta `8501`:
   ```powershell
   .\ngrok.exe http 8501
   ```

## 🧪 Como Testar

- Digite os ingredientes disponíveis e o seu orçamento na barra de chat inferior, **ou**
- Utilize os botões da seção **Testes Rápidos (Avaliação)** na barra lateral para validar automaticamente a criação de receitas, o reaproveitamento de alimentos, a memória de contexto da conversa e o bloqueio de perguntas fora do escopo.

## 🛡️ Restrição de Escopo

O AproveitAI responde apenas sobre receitas, reaproveitamento de alimentos, conservação, combate ao desperdício e compras de alimentos dentro do orçamento. Pedidos fora desse tema (correção de textos, programação, tarefas escolares, assuntos gerais etc.) são bloqueados, o que evita o consumo desnecessário de tokens.

A proteção funciona em três camadas:

1. **Filtro de escopo:** antes da resposta, uma chamada curta ao modelo (sem o histórico completo, com raciocínio mínimo e temperatura 0) classifica a mensagem como `PERMITIDO` ou `BLOQUEADO`.
2. **Resposta fixa:** mensagens bloqueadas recebem uma resposta padrão gerada pelo próprio app, sem acionar o modelo principal. Elas continuam visíveis na conversa, mas não entram no histórico enviado ao modelo.
3. **Instruções do assistente:** o prompt de sistema também restringe o escopo e impede que o assistente mude de papel, como reforço caso algo passe pelo filtro.

Além disso, a caixa de mensagem aceita no máximo 1.000 caracteres.