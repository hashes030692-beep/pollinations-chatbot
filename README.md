# Pollinations Chatbot

A simple browser chatbot powered by [Pollinations.ai](https://pollinations.ai), using **GPT-4o Mini** for text responses and **Flux** for image generation.

## Features

- 💬 Chat with **GPT-4o Mini** (the only text model used — via the Pollinations `openai` route).
- 🖼️ Generate images with **Flux** using the `/image` command.
- 🎨 Clean, responsive single-file UI with no build step or dependencies.

## Usage

1. Open `index.html` in any modern browser.
2. Type a message and press **Enter** to chat.
3. To generate an image, type:

   ```
   /image a neon city at night
   ```

   The image is generated with the Flux model through Pollinations' image API.

## How it works

### Text — GPT-4o Mini

Text requests are sent to the Pollinations text endpoint with `model: "openai"`, which maps to GPT-4o Mini:

```js
const res = await fetch("https://text.pollinations.ai/", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({
    messages: [
      { role: "system", content: "You are a helpful assistant." },
      { role: "user", content: userText }
    ],
    model: "openai" // GPT-4o Mini
  })
});
```

### Images — Flux

Images are generated via the Pollinations image endpoint with `model=flux`:

```
https://image.pollinations.ai/prompt/{prompt}?model=flux&nologo=true&width=768&height=768
```

## Notes

- Only **GPT-4o Mini** (`model: "openai"`) is used for text — no other models.
- Images use the **Flux** model on the Pollinations router.
- No API key, server, or build step required — everything runs in the browser.
