# Google Sheets Form Collector (n8n workflow)

Este flujo en [n8n](https://n8n.io/) permite capturar datos desde un formulario web y guardarlos automáticamente en una hoja de cálculo de Google Sheets.

## 🔧 Requisitos

- Conexión OAuth2 válida a Google Sheets.
- Documento de Google Sheets creado previamente con columnas: `Nombre`, `Email`.

## 🧩 Estructura del flujo

1. `Form Trigger`: Genera un formulario simple.
2. `Append row in sheet`: Guarda los datos en Google Sheets.

## ⚠️ Importante

- Este flujo está **anonimizado**. Debes reemplazar:
  - `YOUR_SPREADSHEET_ID`
  - `YOUR_SHEET_NAME`
  - `REPLACE_WITH_WEBHOOK_ID`
  - Credenciales y versiones
- No compartas tus credenciales reales.

## 🚀 Cómo usarlo

1. Importa el JSON en tu instancia de n8n.
2. Configura las credenciales de Google Sheets.
3. Activa el flujo y prueba el formulario.
