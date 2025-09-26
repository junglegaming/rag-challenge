# Desafio Backend RAG — Sistema de Busca Semântica e Q&A

Bem-vindo(a)! Este é um **teste prático** para a vaga de **AI Developer** na **Jungle Gaming**. O objetivo é avaliar sua capacidade de construir um sistema de Retrieval-Augmented Generation para processar documentos PDF e responder perguntas.

> **Stack Recomendada**
>
> * **Backend:** Python (FastAPI) ou Node.js (Express/Fastify)
> * **Vector Database:** Sua escolha (ChromaDB, Qdrant, Pinecone, Weaviate, etc.)
> * **Embeddings:** Sua escolha (OpenAI, Cohere, HuggingFace, etc.)
> * **LLM:** Sua escolha (OpenAI, Anthropic, Cohere, Ollama, etc.)
> * **Processamento:** LangChain, LlamaIndex ou implementação própria
> * **Infra:** Docker & docker-compose

---

## 🎯 Contexto & Objetivo

Construir uma **API REST de RAG** que processe documentos PDF, faça indexação vetorial, e responda perguntas usando retrieval-augmented generation. O sistema deve retornar respostas contextualizadas com **métricas de confiança**.

**O que queremos observar:**

* Pipeline de processamento e chunking de PDFs
* Qualidade do retrieval (busca semântica)
* Prompt engineering e chain design
* Estrutura e organização do código
* Documentação da API

---

## 🧱 Requisitos Funcionais

### 1. Ingestão de Documentos PDF

* **Upload** de arquivos PDF via API
* **Extração** de texto do PDF
* **Chunking inteligente:**
  * Chunks de tamanho configurável (sugestão: 500 caracteres)
  * Overlap configurável
  * Metadata: filename, chunk_index, timestamp
* **Geração de embeddings** e armazenamento no vector store
* **Resposta com ID do documento** e estatísticas

### 2. Busca e Q&A

* **Endpoint de query** que recebe uma pergunta
* **Busca semântica** nos chunks (top-k configurável)
* **Geração de resposta** usando LLM com contexto
* **Resposta estruturada** contendo:
  * Texto da resposta
  * Confidence score
  * Tokens utilizados (opcional)

### 3. Gerenciamento

* **Listar documentos** processados
* **Health check** do sistema

---

## ⚡ API Endpoints (Obrigatórios)

```http
POST   /api/documents/upload       # Upload de PDF
GET    /api/documents              # Lista documentos

POST   /api/query                  # Pergunta ao sistema

GET    /api/health                 # Status dos componentes
```

### Exemplos de Request/Response

#### Upload de PDF
```bash
POST /api/documents/upload
Content-Type: multipart/form-data

Response:
{
  "document_id": "01998714-4d0d-7620-a18b-5ac0cb775ac1",
  "filename": "manual.pdf",
  "chunks_created": 45
}
```

#### Query RAG
```bash
POST /api/query
{
  "question": "Como configurar o banco de dados?",
  "top_k": 3
}

Response:
{
  "answer": "Para configurar o banco de dados, você deve...",
  "confidence": 0.85,
  "processing_time": 1.2
}
```

---

## 🏗️ Estrutura Sugerida

```
.
├── app/
│   ├── api/              # Endpoints
│   ├── services/         # Lógica de negócio
│   │   ├── pdf_processor.py
│   │   ├── embeddings.py
│   │   └── rag_chain.py
│   ├── config.py
│   └── main.py
├── docker-compose.yml
├── requirements.txt / package.json
├── .env.example
└── README.md
```

---

## 📋 Requisitos Técnicos

### PDF Processing
* **Extração de texto** do PDF
* **Chunking** que não quebre frases no meio
* **Processamento eficiente** de documentos

### Embeddings
* Modelo de sua escolha
* Justifique a escolha no README

### Retrieval
* **Similarity search** 
* **Filtros** por documento quando especificado

### LLM Integration
* **Prompt template** bem estruturado
* **System prompt** instruindo uso de contexto
* **Handling** quando não há contexto relevante

---

## 📝 Critérios de Avaliação

### Obrigatório
- [ ] API funcional com todos endpoints
- [ ] Upload e processamento de PDF
- [ ] Busca semântica funcionando
- [ ] Respostas contextualizadas baseadas nos documentos
- [ ] Docker Compose configurado

### Qualidade
- [ ] Chunking inteligente
- [ ] Prompt engineering eficaz
- [ ] Código limpo e organizado
- [ ] Error handling adequado

### Diferencial
- [ ] Testes automatizados
- [ ] Cache de embeddings
- [ ] Documentação OpenAPI/Swagger
- [ ] Métricas de qualidade do retrieval

---

## 🧪 Teste

Inclua um PDF de exemplo no repositório e algumas queries de teste:

```json
{
  "test_queries": [
    {
      "query": "Pergunta sobre conteúdo específico do PDF",
      "expected_keywords": ["palavra1", "palavra2"]
    }
  ]
}
```

---

## 📚 Documentação Esperada

No README do projeto:

1. **Arquitetura** do sistema
2. **Justificativa** das escolhas técnicas (modelos, chunk size, etc.)
3. **Como rodar** (Docker)
4. **Exemplos de uso** (cURL/Postman)
5. **Limitações e melhorias futuras**

---

## 💡 Dicas

* **Comece simples:** Upload → Chunking → Embeddings → Query
* **PDFs pequenos** para testes iniciais (5-10 páginas)
* **Foque na qualidade** das respostas geradas
* **Documente suas decisões** técnicas

---

## 📧 Suporte e Dúvidas

Caso tenha alguma dúvida sobre o teste ou precise de esclarecimentos:

* Entre em contato com o **recrutador que enviou este teste**
* Ou envie um e-mail para: **recruitment@junglegaming.io**

Responderemos o mais breve possível para garantir que você tenha todas as informações necessárias para realizar o desafio.

---

## 🕒 Prazo

* **Entrega:** 14 dias corridos
* **Formato:** Repositório Git com README completo

**Boa sorte!** 🚀
