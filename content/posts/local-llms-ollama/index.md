---
title: "Running Local LLMs with Ollama: A Developer's Guide"
date: 2026-02-13
draft: false
description: "How to run Llama 3, Mistral, and Gemma locally on your machine using Ollama."
summary: "Stop paying for API credits. Learn how to run state-of-the-art Large Language Models on your own hardware using Ollama."
tags: ["AI", "Ollama", "Local LLMs", "Machine Learning"]
series: ["AI Engineering"]
featuredImage: "https://images.unsplash.com/photo-1620712943543-bcc4688e7485?q=80&w=1965&auto=format&fit=crop"
layout: "simple"
---

{{< lead >}}
Privacy, cost, and latency. Three reasons why **Local LLMs** are the future of AI development. And **Ollama** makes it incredibly easy.
{{< /lead >}}

## What is Ollama?

Ollama is a tool that packages LLMs into easy-to-run binaries. It handles the model weights, the inference engine (llama.cpp), and provides a clean API.

### Getting Started

Install is a one-liner:

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

Run Llama 3:

```bash
ollama run llama3
```

## Building an AI Agent

You can interact with Ollama via a REST API. Here's a simple Python client:

```python
import requests
import json

def chat(prompt):
    url = "http://localhost:11434/api/generate"
    data = {
        "model": "llama3",
        "prompt": prompt,
        "stream": False
    }
    response = requests.post(url, json=data)
    return response.json()['response']

print(chat("Explain quantum computing in one sentence."))
```

{{< alert icon="rocket" >}}
**Pro Tip**: Combine this with **LangChain** or **CrewAI** to build autonomous agents that can browse the web or edit files on your computer.
{{< /alert >}}
