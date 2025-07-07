# 🤖 Telegram Image Analyzer with Google Sheets & OpenAI (n8n Workflow)

![alt text](<Screenshot 2025-07-07 at 1.37.09 PM.png>)

Este flujo de trabajo en **n8n** permite recibir imágenes por Telegram, analizarlas con **OpenAI (GPT-4 Vision)**, registrar el resultado en **Google Sheets** y enviar una respuesta automática al usuario.

---

## 🚀 ¿Qué hace este flujo?

1. 📲 **Recibe una imagen** enviada por un usuario en Telegram.
2. 🧠 **Procesa y analiza la imagen** con el modelo `gpt-4o-mini` u otro compatible.
3. 📝 **Guarda el resultado** en una hoja de cálculo de Google Sheets.
4. 💬 **Responde automáticamente** al usuario de Telegram con la descripción.

---

## 🧩 Componentes del flujo

| Nodo                      | Función                                                          |
| ------------------------- | ---------------------------------------------------------------- |
| `Telegram Trigger`        | Escucha nuevos mensajes con imágenes en Telegram.                |
| `Get a file`              | Descarga la imagen enviada.                                      |
| `Code`                    | Corrige el tipo MIME de la imagen.                               |
| `Analyze image`           | Envía la imagen a OpenAI para analizar su contenido.             |
| `Edit Fields`             | Extrae el resultado de la IA en un campo legible.                |
| `AI Agent`                | Da formato al resultado y genera el mensaje final.               |
| `Append to Google Sheets` | Guarda el resultado en una hoja de cálculo de Google.            |
| `Send a text message`     | Envía al usuario el resultado de lo que se detectó en la imagen. |

---

## ⚙️ Requisitos previos

- ✅ Cuenta de Telegram con un bot creado ([crear uno con @BotFather](https://t.me/BotFather)).
- ✅ Instancia de **n8n** configurada con acceso público (o `n8n.cloud`).
- ✅ Conexión OAuth2 válida con:
  - 🟦 **Telegram** (API Key del bot)
  - 🟩 **Google Sheets** (OAuth con acceso de escritura)
  - 🧠 **OpenAI** (API Key compatible con `gpt-4`, `gpt-4o`, etc.)

---

## 📌 Personalización

1. Reemplaza los siguientes valores en el JSON:

| Campo                           | Reemplazar por                                              |
| ------------------------------- | ----------------------------------------------------------- |
| `"webhookId"`                   | ID generado automáticamente por n8n                         |
| `"telegramApi"` → `id` y `name` | Tus credenciales reales del bot de Telegram                 |
| `"openAiApi"` → `id` y `name`   | Tus credenciales reales de OpenAI                           |
| `"documentId"`                  | ID de tu hoja de cálculo                                    |
| `"sheetName"`                   | GID o nombre de tu hoja                                     |
| `"chatId"`                      | Deja como está si se refiere al usuario que envió la imagen |

2. Verifica que la hoja de cálculo de Google tenga una columna llamada:  
   `¿Qué hay en la imagen?`

---

## 📷 Ejemplo de uso

1. Usuario envía una imagen al bot de Telegram.
2. El flujo analiza la imagen.
3. El bot responde con algo como:
   ¿Qué hay en la imagen?: Se observa un recibo de compra en un supermercado.

Mensaje enviado al usuario: Se observa un recibo de compra en un supermercado.

4. El resultado queda registrado en Google Sheets automáticamente.

---

## 🛡️ Seguridad

🔒 Este flujo no incluye ninguna clave ni token real.  
Antes de subir a producción, asegúrate de:

- No compartir credenciales sensibles.
- Usar permisos mínimos necesarios en tus tokens.

---

## 📎 Recursos útiles

- [Documentación oficial de n8n](https://docs.n8n.io/)
- [Crear un bot de Telegram](https://core.telegram.org/bots)
- [API de Google Sheets](https://developers.google.com/sheets/api)
- [OpenAI Vision](https://platform.openai.com/docs/guides/vision)

---

## 🧠 Autor

Este flujo fue desarrollado como ejemplo educativo para mostrar cómo combinar múltiples herramientas de IA y automatización con **n8n**.

---

## ✨ Licencia

MIT – Libre para usar y modificar.
