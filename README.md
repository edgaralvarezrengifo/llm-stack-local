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

## ▶️ Instrucciones de uso

1. Clonar este repositorio:
   ```bash
   git clone https://github.com/<tu-usuario>/<tu-repo>.git
   cd <tu-repo>
2. Levantar los servicios:
   ```bash
    docker compose up -d
3. Acceder a la interfaz web:
    http://localhost:3000

## 🔧 Servicios
Ollama

- API: http://localhost:11434

- Persistencia en volumen: ollama_data

- Modelo inicial: mistral (se descarga automáticamente la primera vez).

Comandos útiles:

# Ingresar al contenedor
docker exec -it ollama bash

# Listar modelos instalados
ollama list

# Descargar otro modelo
ollama pull llama2

Open WebUI

- Interfaz: http://localhost:3000

- Conexiones configuradas:

    - OLLAMA_BASE_URL=http://ollama:11434

    - MEMORY_BACKEND=qdrant

- Modelo por defecto: mistral

- Configuración avanzada (variables de entorno adicionales):

    - DEFAULT_MODEL → Modelo seleccionado al inicio.

    - MEMORY_BACKEND → Motor de memoria (qdrant, sqlite, etc.).

    - QDRANT_URL → Endpoint de Qdrant.

Qdrant

- API HTTP: http://localhost:6333

- API gRPC: localhost:6334

- Persistencia en volumen: qdrant_data

## 🧪 Caso de uso: RAG (Retrieval Augmented Generation)

1. Carga de documentos en Qdrant mediante embeddings generados por Ollama.

2. Consulta semántica desde Open WebUI:

    - El prompt del usuario se convierte en un embedding.

    - Se busca en Qdrant el contexto más relevante.

    - El contexto se concatena al prompt antes de pasarlo al modelo Mistral.

3. Respuesta final generada con conocimiento aumentado.

## 📚  Referencias

Ollama Docs

Open WebUI

Qdrant Docs

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
