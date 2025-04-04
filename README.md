# Dialogflow-Deepseek
Implementaciòn de API de IA en DialogFlow. *Solo sirve implementado en una API de Mesajeria*
# Finabot - Chatbot Financiero

Finabot es un asistente conversacional para enseñar sobre finanzas. El bot utiliza Dialogflow para manejar las interacciones y DeepSeek para generar respuestas complejas basadas en IA.

## Flujo de Funcionamiento: DeepSeek + Dialogflow

Este proyecto utiliza **Dialogflow** y **DeepSeek** para proporcionar respuestas a preguntas financieras complejas. Aquí te explico cómo trabajan juntos:

### 1. El usuario hace una pregunta
El usuario interactúa con el bot a través de **Telegram**, y por ejemplo pregunta algo relacionado con finanzas, como:

> "¿Qué es el interés compuesto?"

### 2. Dialogflow interpreta la pregunta
**Dialogflow** es un servicio de procesamiento de lenguaje natural que interpreta la intención del usuario. Detecta que la intención es **"ConsultaFinanzas"** y pasa la pregunta a nuestro backend.

### 3. Consulta a DeepSeek
El backend envía la consulta a **DeepSeek**, un modelo de IA entrenado específicamente para responder preguntas financieras. El sistema recibe la siguiente solicitud:

```javascript
let response = await axios.post(
  "https://api.deepseek.com/v1/chat/completions",
  {
    model: "deepseek-chat",
    messages: [
      { role: "system", content: "Eres Finabot, un chatbot asistente financiero. No puedes contestar sobre otros temas." },
      { role: "user", content: consulta },
    ],
    max_tokens: 200,
  },
  {
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer <tu_api_key>`, // Aquí debes colocar tu clave de API de DeepSeek
    }
  }
);
