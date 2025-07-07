# 🔍 RAG Workflow with n8n + Google Drive + OpenAI + Pinecone

Este flujo de trabajo en **n8n** implementa una arquitectura RAG (Retrieval-Augmented Generation) para subir documentos a una base vectorial (Pinecone) y permitir consultas en lenguaje natural mediante un agente inteligente potenciado con OpenAI.

---

## 🧠 ¿Qué hace este flujo?

1. 🗂 **Monitorea una carpeta de Google Drive**.
2. 📥 Cuando se sube un archivo nuevo, lo descarga.
3. 🧾 Lo procesa (carga, divide, genera embeddings).
4. 🧬 Inserta los vectores en un índice de Pinecone.
5. 💬 Un agente de IA espera mensajes de texto (tipo chatbot).
6. 🔍 El agente consulta la base vectorial para responder preguntas sobre los documentos.
7. 📚 La IA responde con contexto basado únicamente en los documentos cargados.

---

## 🔧 Requisitos

### Cuentas necesarias

- ✅ [n8n](https://n8n.io/)
- ✅ Google Drive con carpeta dedicada
- ✅ [OpenAI API Key](https://platform.openai.com/)
- ✅ [Pinecone](https://www.pinecone.io/) con índice configurado

### Credenciales en n8n

- `googleDriveOAuth2Api`: acceso de lectura a la carpeta.
- `openAiApi`: clave API de OpenAI (gpt-3.5 o gpt-4).
- `pineconeApi`: clave API de Pinecone y nombre del índice.

---

## 📁 Flujo de carga (Ingesta)

| Nodo                                           | Función                                         |
| ---------------------------------------------- | ----------------------------------------------- |
| `Google Drive Trigger`                         | Detecta cuando se sube un nuevo archivo.        |
| `Download file`                                | Descarga el archivo desde Google Drive.         |
| `Recursive Character Splitter` → `Data Loader` | Divide el contenido en fragmentos y lo prepara. |
| `Embeddings OpenAI`                            | Genera los embeddings de los fragmentos.        |
| `Pinecone Vector Store`                        | Inserta los vectores en el índice.              |

---

## 🤖 Flujo de consulta (Chat)

| Nodo                         | Función                                                         |
| ---------------------------- | --------------------------------------------------------------- |
| `When chat message received` | Recibe la consulta del usuario.                                 |
| `AI Agent`                   | Interpreta la pregunta, consulta en Pinecone y responde.        |
| `Pinecone Vector Store1`     | Devuelve los fragmentos más relevantes desde la base vectorial. |
| `Simple Memory`              | Guarda el historial breve de conversación (opcional).           |

---

## 💬 Ejemplo de uso

1. **Subes un PDF** a la carpeta "Biblioteca RAG" en Google Drive.
2. El documento se procesa y se guarda como vectores en Pinecone.
3. El usuario escribe: `¿Qué ingredientes contiene el serum revitalizante?`
4. El flujo:
   - Busca la respuesta en Pinecone.
   - Construye una respuesta coherente y con fuente.
   - Responde:  
     `El serum contiene ácido hialurónico, vitamina C y extracto de algas. (Fuente: ingredientes_serum.pdf)`

---

## 🛡️ Seguridad

🔐 Este flujo no contiene claves API ni IDs sensibles.

- Anonimiza:
  - IDs de carpetas de Google Drive.
  - Nombres de credenciales.
  - Índices de Pinecone.
- Usa variables de entorno o credenciales seguras en producción.

---

## ⚙️ Personalización

- Cambia el modelo (`gpt-3.5-turbo`, `gpt-4`) si usas OpenAI.
- Modifica el `systemMessage` en el `AI Agent` para personalizar el tono o propósito del asistente.
- Ajusta el `topK` en Pinecone si deseas más o menos resultados por consulta.

---

## 📚 Recursos

- [Pinecone para desarrolladores](https://docs.pinecone.io/)
- [OpenAI con n8n](https://docs.n8n.io/integrations/builtin/openai/)
- [RAG con LangChain](https://docs.langchain.com/docs/use-cases/question-answering/)

---

## 🧑‍💻 Autor

Desarrollado como ejemplo de arquitectura RAG automatizada para casos de uso como:

- Soporte técnico
- Documentación interna
- FAQs sobre productos

---

## 📄 Licencia

MIT – Puedes usarlo, modificarlo o compartirlo libremente.  
Si te resulta útil, ¡déjanos un ⭐ en el repositorio!
