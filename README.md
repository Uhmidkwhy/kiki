# KIKI

A minimalist dark-mode chat app with streaming LLM responses and an animated cat companion in the corner.

## Tech stack

- **Frontend:** Next.js 15 (App Router), React 19, Tailwind CSS 4, shadcn/ui
- **AI:** Next.js Route Handlers via [Vercel AI SDK](https://sdk.vercel.ai/) — OpenAI, Anthropic, or local Ollama (OpenAI-compatible)
- **Animation:** Framer Motion (60fps cat states)
- **State:** React hooks + `localStorage` for settings and chat history

## Project structure

```
.
├── public/                    # Static assets
├── src/
│   ├── app/
│   │   ├── api/chat/        # Streaming chat route (Step 2)
│   │   ├── globals.css      # Tailwind + shadcn theme (dark default)
│   │   ├── layout.tsx
│   │   └── page.tsx
│   ├── components/
│   │   ├── ui/              # shadcn primitives
│   │   ├── chat/            # Sidebar, messages, input
│   │   ├── settings/        # Settings sheet
│   │   └── cat/             # SVG cat + mood animations
│   ├── hooks/               # useChat, useSettings, useCatMood
│   └── lib/
│       ├── ai/
│       │   ├── errors.ts
│       │   └── providers.ts
│       ├── chat-request.ts  # Zod schema + message helpers
│       ├── utils.ts
│       ├── types.ts
│       └── settings.ts      # localStorage helpers (Step 3)
├── .env.example
├── components.json          # shadcn CLI config
├── next.config.ts
├── package.json
├── postcss.config.mjs
└── tsconfig.json
```

## Getting started

### 1. Install dependencies

```bash
npm install
```

### 2. Environment variables

Copy the example file and fill in keys for your chosen provider:

```bash
cp .env.example .env.local
```

| Variable | Description |
|----------|-------------|
| `AI_PROVIDER` | `openai` \| `anthropic` \| `ollama` |
| `OPENAI_API_KEY` | OpenAI API key |
| `ANTHROPIC_API_KEY` | Anthropic API key |
| `OLLAMA_BASE_URL` | Default `http://localhost:11434/v1` |

Settings in the UI can override provider, model, temperature, system prompt, and API keys (stored in the browser).

### Cat companion moods

The corner cat reacts to chat state (Framer Motion, GPU-friendly transforms):

| Mood | When |
|------|------|
| `idle` | Default — slow blink, whisker twitch |
| `thinking` | Waiting for first token — scribble spins above head |
| `streaming` | Tokens arriving — bob + whisker motion + mouth line |
| `success` | Reply finished — bounce, both eyes open briefly |
| `error` | API/config failure — shake + red stroke + frantic scribble |

Respects `prefers-reduced-motion` (falls back to calm idle).

### 3. Run the dev server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

### 4. Ollama (optional)

```bash
ollama pull llama3.2
ollama serve
```

Set `AI_PROVIDER=ollama` in `.env.local` or pick Ollama in Settings.

## Build

```bash
npm run build
npm start
```

## Chat API (`POST /api/chat`)

Streaming endpoint compatible with the Vercel AI SDK `useChat` hook (Step 3).

**Request body (JSON):**

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `messages` | `{ role, content }[]` | yes | At least one `user` message |
| `provider` | `openai` \| `anthropic` \| `ollama` | no | Defaults to `AI_PROVIDER` env |
| `model` | string | no | Provider-specific default if omitted |
| `temperature` | 0–2 | no | Default `0.7` |
| `systemPrompt` | string | no | Overrides env / built-in KIKI prompt |
| `openaiApiKey` | string | no | Overrides `OPENAI_API_KEY` |
| `anthropicApiKey` | string | no | Overrides `ANTHROPIC_API_KEY` |
| `ollamaBaseUrl` | string | no | Overrides `OLLAMA_BASE_URL` |

**Success:** `text/event-stream` data stream (AI SDK protocol).

**Errors:** JSON `{ error, code }` with HTTP 400 (validation/config), 502 (provider), or 500.

**Quick test (after `npm run dev`):**

```bash
curl -N http://localhost:3000/api/chat \
  -H "Content-Type: application/json" \
  -d "{\"messages\":[{\"role\":\"user\",\"content\":\"Say hi in one sentence.\"}]}"
```

## Implementation steps

1. **Step 1 (done):** Config, layout, theme, types, folder scaffold
2. **Step 2 (done):** `/api/chat` streaming route + provider wiring
3. **Step 3 (done):** Chat UI, sidebar history, settings panel, shadcn components
4. **Step 4 (done):** Cat companion (SVG + Framer Motion moods at 60fps)

## License

MIT
