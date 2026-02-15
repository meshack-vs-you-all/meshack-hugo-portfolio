---
title: "Running Local LLMs with Ollama: A Developer's Guide"
date: 2026-02-13
draft: false
description: "How to run Llama 3, Mistral, and Gemma locally on your machine using Ollama. Includes building a RAG pipeline."
summary: "Stop paying for API credits. Learn how to run state-of-the-art Large Language Models on your own hardware using Ollama."
tags: ["AI", "Ollama", "Local LLMs", "Machine Learning"]
series: ["AI Engineering"]
featuredImage: "https://images.unsplash.com/photo-1620712943543-bcc4688e7485?q=80&w=1965&auto=format&fit=crop"
layout: "simple"
---

{{< lead >}}
Privacy, cost, and latency. Three reasons why **Local LLMs** are the future of AI development. And **Ollama** makes it incredibly easy.
{{< /lead >}}

## 1. What is Ollama?

Ollama is a tool that packages LLMs into easy-to-run binaries. It handles the model weights, the inference engine (llama.cpp), and provides a clean API.

### Getting Started

Install is a one-liner:

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

Run Llama 3 (8 Billion Parameters):

```bash
ollama run llama3
```

## 2. Integrating with Python

You can interact with Ollama via a REST API. Here's a clean client:

```python
import requests
import json

def chat(prompt, model="llama3"):
    url = "http://localhost:11434/api/generate"
    data = {
        "model": model,
        "prompt": prompt,
        "stream": False
    }
    response = requests.post(url, json=data)
    return response.json()['response']

print(chat("Explain quantum computing in one sentence."))
```

## 3. Building a RAG Pipeline (Retrieval Augmented Generation)

The real power comes when you give the LLM your own data.

### The Stack
-   **Ollama**: Inference
-   **ChromaDB**: Vector Store
-   **LangChain**: Glue code

```python
from langchain_community.llms import Ollama
from langchain_community.document_loaders import TextLoader
from langchain_community.embeddings import OllamaEmbeddings
from langchain_community.vectorstores import Chroma

# 1. Load Data
loader = TextLoader("my_notes.txt")
docs = loader.load()

# 2. Embed Data (Turn text into numbers)
embeddings = OllamaEmbeddings(model="llama3")
db = Chroma.from_documents(docs, embeddings)

# 3. Query
query = "What did I say about productivity?"
docs = db.similarity_search(query)

# 4. Ask LLM
llm = Ollama(model="llama3")
answer = llm.invoke(f"Context: {docs[0].page_content}. Question: {query}")
print(answer)
```

{{< alert icon="rocket" >}}
**Pro Tip**: This runs 100% offline. You can build a personal assistant that knows your private notes without ever sending data to OpenAI.
{{< /alert >}}

## 4. Hardware Requirements

-   **RAM**:
    -   7B Models (Llama 3, Mistral): Needs ~8GB RAM.
    -   13B Models: Needs ~16GB RAM.
    -   70B Models: Needs ~48GB RAM (Mac Studio / Dual GPU).
-   **GPU**: Nvidia is best, but Apple Silicon (M1/M2/M3) is surprisingly fast due to Unified Memory.
