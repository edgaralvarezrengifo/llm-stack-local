# llm-stack-local

# 🧠 Implementación de agentes de IA con LLMs locales open source

Este repositorio contiene la implementación de un entorno de **IA local** para el caso de uso  

**interacción con modelos de lenguaje y recuperación aumentada (RAG)**.  

que hace parte del proyecto de grado **"Implementación de agentes de IA con LLMs locales en entornos seguros"** de la **Pontificia Universidad Javeriana**.

La arquitectura se basa en tres componentes principales:

- **[Ollama](https://ollama.ai/)** → Motor para ejecutar modelos de lenguaje grandes (**LLMs**) localmente.
- **[Open WebUI](https://github.com/open-webui/open-webui)** → Interfaz web para interacción con LLMs y gestión de memoria.
- **[Qdrant](https://qdrant.tech/)** → Base de datos vectorial para almacenamiento y búsqueda semántica de embeddings.

El modelo configurado por defecto es **Mistral**, un LLM ligero y eficiente, ideal para entornos con recursos limitados.

---

## ⚙️ Arquitectura de la solución

```mermaid
flowchart LR
    subgraph User["👤 Usuario"]
      A[Open WebUI] -->|prompt| B[Ollama]
      A -->|consulta semántica| C[Qdrant]
    end

    subgraph Backend["🖥️ Backend Local"]
      B[Ollama] -->|respuesta| A
      C[Qdrant] -->|documentos relevantes| A
    end
