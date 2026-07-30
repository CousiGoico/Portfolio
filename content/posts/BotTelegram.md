---
title: "Guía Completa: Crear un Bot de Telegram con C# (.NET)"
date: 2026-05-03T00:00:00+00:00
cover: /img/telegram-logo.webp
---

# 🤖 Guía Completa: Crear un Bot de Telegram con C# (.NET)

## 📌 Introducción

Telegram ofrece una API muy potente para crear bots que pueden automatizar tareas, responder usuarios, integrarse con servicios externos y mucho más. En esta guía aprenderás paso a paso cómo crear un bot usando C# con .NET, desde cero hasta un nivel práctico.

---

## 🧰 Requisitos

- .NET SDK instalado (recomendado .NET 6 o superior)
- Conocimientos básicos de C#
- Cuenta de Telegram

---

## 🧑‍💻 1. Crear el bot y obtener el TOKEN

### Paso 1: Abrir BotFather

1. En Telegram, busca: `@BotFather`
2. Inicia una conversación

### Paso 2: Crear el bot

Escribe:

        /newbot

BotFather te pedirá:
- Nombre del bot (ej: `Mi Bot`)
- Username único (debe terminar en `bot`, ej: `mi_bot_123_bot`)

### Paso 3: Obtener el TOKEN

Recibirás algo como:

        123456789:ABCdefGhIJKlmNoPQRsTUVwxyZ


⚠️ **IMPORTANTE:** Este token es privado. No lo compartas.

---

## 🆔 2. Obtener el CHAT ID

El `chat_id` es necesario para enviar mensajes a usuarios o grupos.

### Método 1: Usando un bot auxiliar

1. Envía un mensaje a tu bot recién creado
2. Abre en el navegador:

`https://api.telegram.org/bot<TU_TOKEN>/getUpdates`

Ejemplo:

[https://api.telegram.org/bot123456:ABC/getUpdates](https://api.telegram.org/bot123456:ABC/getUpdates)

3. Verás un JSON como este:

```json
{
  "result": [
    {
      "message": {
        "chat": {
          "id": 123456789,  // Chat id
          "first_name": "TuNombre"
        }
      }
    }
  ]
}
```

### Método 2: Usar un bot tipo "userinfobot"

Simplemente busca un bot que te diga tu ID y listo.

---

## 🏗️ 3. Crear el proyecto en C#

1. Abre tu terminal y crea un nuevo proyecto:

```bash
dotnet new console -n TelegramBot
cd TelegramBot
```

2. Agrega el paquete NuGet para Telegram.Bot:

```bash
dotnet add package Telegram.Bot
```

## 🧑‍💻 4. Código para enviar un mensaje

Abre el archivo `Program.cs` y reemplázalo con el siguiente código:

```csharp
using System;
using System.Threading.Tasks;
using Telegram.Bot;

class Program
{
    static async Task Main(string[] args)
    {
        var botClient = new TelegramBotClient("TU_TOKEN_AQUI");

        var chatId = "TU_CHAT_ID_AQUI";
        var message = "¡Hola, mundo!";

        await botClient.SendTextMessageAsync(chatId, message);

        Console.WriteLine("Mensaje enviado.");
    }
}
```

### Reemplaza `TU_TOKEN_AQUI` y `TU_CHAT_ID_AQUI` con los valores que obtuviste anteriormente.

## 🚀 5. Ejecutar el bot

En la terminal, ejecuta:

```bash
dotnet run
```

Si todo está correcto, deberías recibir el mensaje "¡Hola, mundo!" en tu Telegram.

---

## 🧑‍💻 6. Mejoras y funcionalidades adicionales

- Responder a mensajes entrantes
- Enviar imágenes, documentos, etc.
- Integrar con APIs externas
- Manejar comandos personalizados

---

## 🔁 7. Long Polling vs Webhooks

✔ Long Polling (recomendado para empezar)

- El bot consulta constantemente a Telegram
- Fácil de implementar
- No requiere servidor público

✔ Webhooks (producción)

- Telegram envía eventos a tu servidor
- Más eficiente
- Requiere HTTPS

### 🧠 Comandos básicos

```csharp
if (text.StartsWith("/start"))
{
    await bot.SendTextMessageAsync(chatId, "Bienvenido!");
}
else if (text.StartsWith("/help"))
{
    await bot.SendTextMessageAsync(chatId, "Comandos disponibles: /start, /help");
}
```

---

## 📊 8. Manejo de errores y buenas prácticas

- Manejar excepciones
- Validar entradas
- Registrar logs
- Implementar reintentos

---

## 🛠️ 9. Despliegue

Para producción, puedes desplegar tu bot en servicios como:

- Azure
- AWS
- Heroku
- VPS propio
- Docker
- etc.

---

## 📚 Recursos adicionales

- [Telegram Bot API Documentation](https://core.telegram.org/bots/api)
- [Telegram.Bot NuGet Package](https://www.nuget.org/packages/Telegram.Bot/)
