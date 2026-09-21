# Criando um Assistente de Investimentos com RPA e IA Generativa

## Descrição

Aprenda na prática como criar um fluxo de automação inteligente combinando técnicas de RPA (Robotic Process Automation) com workflows de IA no N8N.

Neste desafio, você vai construir um assistente de investimentos automatizado. O fluxo começa com a extração de dados de clientes em uma página web usando Python, passa pela orquestração de um workflow no N8N e termina com a geração de mensagens personalizadas para cada perfil de investidor.

O projeto foi pensado para ser simples e acessível, mesmo para quem está dando os primeiros passos em Python e automação. A ideia é que você entenda o conceito de RPA de forma leve e aplique tudo em um cenário realista do mercado financeiro.

## Objetivo do Projeto

Desenvolver um pipeline de automação que:

1. **Coleta dados de clientes** de uma página web simulada usando Python
2. **Processa as informações** através de um workflow no N8N
3. **Cruza perfis de investidor** com uma base de opções de investimento
4. **Gera mensagens personalizadas** para cada cliente

Ao final, você terá um sistema funcional que demonstra como empresas do setor financeiro podem automatizar a comunicação com clientes de forma inteligente.

## Arquitetura do Projeto

```mermaid
flowchart LR
  %% Pipeline RPA + N8N + IA (máx. 7 caixinhas)

  subgraph GH["GitHub Pages"]
    A["Clientes<br>(docs/index.html)"]
    E["Investimentos (docs/data.csv)"]
  end

  subgraph PY["RPA (Python)"]
    B["Extrair Clientes"]
  end

  subgraph N8["N8N (Workflow)"]
    C["Webhook<br>(Entrada)"]
    D["Cruzar Dados<br>(Clientes x Investimentos)"]
    M["Gerar Mensagem<br>(Template/LLM)"]
    C --> D --> M
  end

  subgraph OUT["Saída"]
    O["Mensagens Personalizadas"]
  end

  A <-->|HTTP| B --> C
  E <-->|HTTP| D
  M --> O

  %% Estilos
  classDef source fill:#E3F2FD,stroke:#1E88E5,stroke-width:1px,color:#0D47A1;
  classDef rpa fill:#E8F5E9,stroke:#43A047,stroke-width:1px,color:#1B5E20;
  classDef n8n fill:#FFF3E0,stroke:#FB8C00,stroke-width:1px,color:#E65100;
  classDef out fill:#FCE4EC,stroke:#D81B60,stroke-width:1px,color:#880E4F;

  class A,E source;
  class B rpa;
  class C,D,M n8n;
  class O out;

```

## Tecnologias e Ferramentas

O projeto utiliza ferramentas gratuitas e acessíveis, organizadas conforme cada etapa do fluxo:

| Etapa | Ferramenta | Função |
|-------|-----------|--------|
| Hospedagem | GitHub Pages | Servir a página de clientes e o CSV de investimentos |
| Extração (RPA) | Python + BeautifulSoup | Coletar dados dos clientes via web scraping |
| Orquestração | N8N | Processar dados, cruzar perfis e gerar mensagens |
| Geração com IA | Agente de IA no N8N | Criar mensagens personalizadas com LLM (desafio extra) |

Além dessas, você pode usar IAs generativas como **Gemini**, **Claude** ou **ChatGPT** como copilotos para auxiliar na escrita de código e tirar dúvidas ao longo do desenvolvimento.

## Roteiro do Desafio

### Etapa 1: Entenda o Projeto

Antes de começar, explore o repositório base que já contém a estrutura inicial:

1. **Página de Clientes (`docs/index.html`):** Uma página HTML hospedada no GitHub Pages com uma lista de clientes fictícios contendo nome, email, saldo e perfil de investidor (Conservador, Moderado ou Arrojado). Disponível online [neste link](https://digitalinnovationone.github.io/dio-lab-assistente-investimentos-rpa-n8n).
2. **Dados de Investimentos (`docs/data.csv`):** Um arquivo CSV também hospedado no GitHub Pages com opções de investimento organizadas por perfil. Disponível online [neste link](https://digitalinnovationone.github.io/dio-lab-assistente-investimentos-rpa-n8n/data.csv).
3. **Script de RPA (`src/extrair_clientes.ipynb`):** Um notebook Python que acessa a página de clientes e extrai os dados da tabela usando BeautifulSoup.

> 🤖 **Por que o script é considerado RPA?** Ele faz exatamente o que um humano faria manualmente: abre uma página, lê os dados de uma tabela e os envia para outro sistema. A diferença é que o "robô" (código) executa isso automaticamente. Essa abordagem é útil quando não existe uma API disponível ou quando precisamos integrar sistemas legados.

### Etapa 2: Configure o Ambiente

1. Faça um **fork** do repositório base para sua conta do GitHub
2. Crie uma conta no [N8N Cloud](https://n8n.io/) ou instale localmente
3. Abra o notebook `src/extrair_clientes.ipynb` no [Google Colab](https://colab.research.google.com/) e execute para entender o fluxo de extração

> 💡 **Atenção:** O script já extrai os dados, mas o envio ao N8N está comentado (`TODO`). Você vai configurar a URL do Webhook após criá-lo na próxima etapa.

### Etapa 3: Desenvolva o Workflow no N8N

Este é o coração do desafio! Monte um fluxo que:

1. Receba os dados dos clientes via Webhook (copie a URL gerada e configure no script Python)
2. Leia o arquivo `docs/data.csv` com as opções de investimento
3. Cruze o perfil de cada cliente com a opção adequada
4. Gere uma mensagem de recomendação para cada cliente

### Etapa 4 (MVP): Mensagens Estáticas

Para a versão mínima, use templates de mensagem fixos baseados no perfil:

- **Conservador:** Foco em renda fixa e segurança
- **Moderado:** Mix equilibrado entre renda fixa e variável
- **Arrojado:** Ênfase em ações e maior potencial de retorno

### Etapa 5 (Desafio): Integração com IA Generativa

Conecte o Agente de IA do N8N a um modelo como Gemini ou GPT para:

- Analisar o contexto do cliente (saldo, perfil)
- Gerar mensagens únicas e personalizadas
- Criar recomendações mais inteligentes e humanizadas

## Entregáveis

### MVP (Mínimo Viável)

- [ ] Repositório forkado com o workflow N8N implementado
- [ ] Workflow N8N exportado (`n8n/workflow.json`) com mensagens estáticas
- [ ] Script de RPA integrado ao Webhook do N8N
- [ ] Print ou vídeo demonstrando o fluxo funcionando de ponta a ponta

### Desafio Completo

- [ ] Todos os itens do MVP
- [ ] Integração com Agente de IA no N8N
- [ ] Mensagens geradas dinamicamente via LLM
- [ ] Documentação explicando as decisões técnicas

## Estrutura do Repositório

```
📁 dio-lab-assistente-investimentos-rpa-n8n/
├── 📄 README.md
├── 📁 src/
│   └── 📄 extrair_clientes.ipynb   # ✅ Notebook Python (já implementado, falta só o TODO)
├── 📁 n8n/
│   └── 📄 workflow.json            # 🎯 Seu desafio: exportar o workflow aqui
└── 📁 docs/
    ├── 📄 index.html               # ✅ Página de clientes (já implementado)
    └── 📄 data.csv                 # ✅ Opções de investimento (já implementado)
```

## Prompts Úteis para Copilotos de IA

| Tarefa | Sugestão de Prompt |
|--------|-------------------|
| Gerar dados fictícios | "Crie 10 clientes fictícios com nome, email, saldo e perfil de investidor em JSON" |
| Entender código | "Explique o que faz a biblioteca BeautifulSoup em Python" |
| Debugar erros | "Meu script Python está dando erro X, o que pode ser?" |
| Montar workflow | "Como configuro um webhook no N8N para receber dados JSON?" |

## Referências

- [Documentação do N8N](https://docs.n8n.io/)
- [BeautifulSoup: Web Scraping com Python](https://realpython.com/beautiful-soup-web-scraper-python/)
- [GitHub Pages: Guia Rápido](https://pages.github.com/)

---

**Bons estudos e mãos à obra** 🚀

Se tiver dúvidas, lembre-se: a melhor forma de aprender é experimentando. Erre, corrija e celebre cada pequena vitória no caminho.

---

## 🚀 Implementação Prática, Desafios e Evolução do Projeto

Nesta seção, apresento os detalhes técnicos da implementação completa do projeto, destacando a arquitetura final, os desafios superados e as melhorias enterprise adicionadas ao fluxo.

### 📜 Nome do Workflow
**`RPA-AI-Investment-Assistant-Workflow`**

---

### 💡 Desafios Encontrados e Soluções Aplicadas

Durante o desenvolvimento da automação de ponta a ponta, diversos cenários reais de integração exigiram ajustes técnicos:

1. **Exposição da Instância Local do n8n:**
   - *Desafio:* O notebook do Google Colab (Python) precisava enviar os dados raspados via POST para o Webhook do n8n rodando localmente.
   - *Solução:* Utilização do `localtunnel` (`npx localtunnel --port 5678`) com o cabeçalho `bypass-tunnel-reminder: true` configurado nas requisições HTTP, garantindo conectividade estável sem bloqueios de tela intermediária.

2. **Geração e Parsing de JSON Estruturado pela IA:**
   - *Desafio:* O LLM (Google Gemini Flash) retornava respostas com marcações Markdown (` ```json `), que quebravam a execução direta de nós subsequentes.
   - *Solução:* Implementação de um nó de código JavaScript customizado utilizando Expressões Regulares (`replace(/```json\s*/g, '')`) e `JSON.parse()`, garantindo que os campos `subject`, `text_body` e `html_body` fossem limpos e extraídos corretamente.

3. **Validação de E-mails Fictícios:**
   - *Desafio:* A base de clientes continha endereços de e-mail inválidos que causavam falhas diretas nas requisições da API do Gmail.
   - *Solução:* Adição de um nó condicional (`If`) com validação por Expressão Regular (Regex: `^[^\s@]+@[^\s@]+\.[^\s@]+$`), desviando e-mails malformados do nó de envio e evitando interrupções no fluxo.

4. **Permissões de API e Localização de Planilhas:**
   - *Desafio:* Erro de permissão ao tentar interagir com o Google Sheets no n8n (`Google Drive API has not been used in project...`).
   - *Solução:* Ativação da **Google Drive API** e **Google Sheets API** no Google Cloud Console, permitindo que a integração consulte e edite planilhas por nome e ID.

---

### ✨ Diferenciais e Melhorias Implementadas (Enterprise Ready)

Além dos requisitos solicitados no desafio original, o projeto foi expandido para um nível de produção comercial:

* **Auditoria Completa e Registro de Logs (Google Sheets):**
  - Integração com o Google Sheets (`Append Row`) conectada a **ambos os caminhos do fluxo**:
    - **Caminho Sucesso (TRUE):** Envia o e-mail via Gmail e grava a linha na planilha com status `Enviado`.
    - **Caminho Falha (FALSE):** Ignora o envio do e-mail e grava o evento diretamente na planilha com status `E-mail Inválido`.
  - Isso garante rastro de auditoria sem perder dados de nenhum cliente da base.

* **Organização Visual por Áreas (Sticky Notes):**
  - O fluxo no n8n foi visualmente estruturado com blocos organizacionais (Post-its coloridos) e renomeado com padronização técnica:
    1. **1. CAPTURA E CONSOLIDAÇÃO DE DADOS** *(Webhook, HTTP Request, Merge e Parsing)*
    2. **2. PROCESSAMENTO E I.A** *(Regras de negócio, montagem de prompts, execução do Gemini e tratamento da resposta)*
    3. **3. VALIDAÇÃO DE DADOS** *(Filtro Regex de e-mail)*
    4. **4. DISPARO, AUDITORIA E RESPOSTA** *(Gmail, Logs no Sheets e Response ao Webhook)*

---

## 🛠️ Tecnologias Adicionais Utilizadas

- **n8n Community Edition** (Orquestração do fluxo)
- **Google Gemini API (`gemini-flash-latest`)** (Geração de cópia personalizada de e-mail)
- **Gmail OAuth2 API** (Disparo automatizado de e-mails)
- **Google Sheets API & Google Drive API** (Auditoria e geração de logs)
- **localtunnel** (Exposição de Webhook em ambiente dev)

---

## 👨‍💻 Autor

Desenvolvido por **Seu Nome Aqui**. Entre em contato ou acompanhe meus projetos:

- 💼 **LinkedIn:** [(https://www.linkedin.com/in/caio-bauab-032189206/)](https://www.linkedin.com/)
- 🐙 **GitHub:** [https://github.com/Caiobauab360](https://github.com/)
- 🌐 **Portfólio (GitHub Pages):** [(https://caiobauab360.github.io/)](https://github.com/)

