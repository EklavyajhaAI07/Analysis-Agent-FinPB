<div align="center">

# 🇮🇳 FinPlay Bharat Analysis Engine

### *Your AI-Powered Financial Intelligence Chat Interface*

<br/>

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![TailwindCSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)
![Claude](https://img.shields.io/badge/Claude-D97757?style=for-the-badge&logo=claude&logoColor=white)
![Gemini](https://img.shields.io/badge/Gemini-8E75B2?style=for-the-badge&logo=googlegemini&logoColor=white)
![ChatGPT](https://img.shields.io/badge/ChatGPT-74aa9c?style=for-the-badge&logo=openai&logoColor=white)
![OpenRouter](https://img.shields.io/badge/OpenRouter-6E3AFA?style=for-the-badge&logo=openai&logoColor=white)

![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)
![Status](https://img.shields.io/badge/status-active-brightgreen?style=flat-square)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-orange?style=flat-square)
![Single File](https://img.shields.io/badge/build-single--file-purple?style=flat-square)

</div>

---

## 📖 Table of Contents

- [Overview](#-overview)
- [Live Demo](#-live-demo)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [How It Works](#-how-it-works)
- [Getting Started](#-getting-started)
- [Configuration](#-configuration)
- [Project Structure](#-project-structure)
- [Architecture Decisions](#-architecture-decisions)
- [Pros & Cons Analysis](#-pros--cons-analysis)
- [Roadmap](#-roadmap)
- [Contributing](#-contributing)

---

## 🌟 Overview

**FinPlay Bharat Analysis Engine** is a sleek, single-file AI chatbot interface purpose-built for financial analysis in the Indian market context. It connects to powerful LLMs via [OpenRouter](https://openrouter.ai), enabling real-time streaming conversations with full chat history management — all in one self-contained HTML file.

> 💡 **No backend. No build step. No frameworks to install.** Just open the HTML file in a browser and start analyzing.

---

## 🚀 Live Demo

```
1. Download index.html
2. Open in any modern browser
3. Add your OpenRouter API key in ⚙ Settings
4. Start chatting!
```

---

## ✨ Features

| Feature | Description |
|---|---|
| 🤖 **AI Streaming** | Real-time token-by-token response streaming via OpenRouter API |
| 💬 **Multi-Chat** | Create, switch, and manage unlimited chat sessions |
| 🌙 **Dark Mode** | Full dark/light theme toggle with localStorage persistence |
| 📱 **Responsive** | Mobile-first sidebar with smooth slide-in/out transitions |
| ⚙️ **Configurable** | Set API key, model, and system prompt per-chat via Settings modal |
| 📝 **Markdown** | Full markdown rendering (code blocks, tables, bold, etc.) via `marked.js` |
| 💾 **Persistent** | All chats and settings saved to `localStorage` — survive page refresh |
| 🔒 **Private** | Everything runs client-side — your API key never hits a third-party server |

---

## 🛠 Tech Stack

```
┌─────────────────────────────────────────────────┐
│             FinPlay Bharat Stack                │
│                                                 │
│  📄  HTML5          → Structure & Layout        │
│  🎨  Tailwind CSS   → Utility-first Styling     │
│  ⚡  Vanilla JS     → All Logic (IIFE pattern)  │
│  📦  marked.js      → Markdown → HTML parsing   │
│  🤖  OpenRouter API → LLM Gateway (Claude etc.) │
│  💾  localStorage   → State Persistence         │
└─────────────────────────────────────────────────┘
```

### External CDNs Used

```html
<!-- Tailwind CSS (styling) -->
<script src="https://cdn.tailwindcss.com"></script>

<!-- Marked.js (markdown rendering) -->
<script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
```

---

## ⚙️ How It Works

```
User types message
       │
       ▼
  sendMessage()
       │
       ├──► Pushes to chat.messages[]
       │
       ├──► POST to OpenRouter API
       │         (stream: true)
       │
       ▼
  ReadableStream reader
       │
       ├──► Decode SSE chunks → parse delta tokens
       │
       ├──► Live-update bubble (textContent)
       │
       └──► On [DONE] → marked.parse() → innerHTML
                │
                └──► saveState() → localStorage
```

**Server-Sent Events (SSE) Streaming Flow:**
1. `fetch()` sends the full message history to OpenRouter
2. Response body is read as a `ReadableStream`
3. Each chunk is decoded, split by newlines, and filtered for `data:` prefixes
4. JSON is parsed, delta tokens extracted and appended to the bubble live
5. On stream completion, the raw text is rendered as Markdown

---

## 🚀 Getting Started

### Prerequisites

- A modern browser (Chrome, Firefox, Edge, Safari)
- An [OpenRouter API Key](https://openrouter.ai/keys) (free tier available)

### Setup — 3 Steps

```bash
# Step 1: Download or clone
git clone https://github.com/your-username/finplay-bharat.git

# Step 2: Open the file
open index.html    # macOS
start index.html   # Windows
xdg-open index.html # Linux

# Step 3: Configure
# Click ⚙ Settings → paste your OpenRouter API Key → Save
```

---

## 🔧 Configuration

Open **Settings** (⚙ icon in sidebar) to configure:

| Setting | Default | Description |
|---|---|---|
| `API Key` | *(empty)* | Your OpenRouter API key |
| `Model` | `anthropic/claude-3.5-sonnet` | Any OpenRouter-supported model |
| `System Prompt` | *(empty)* | Per-chat persona/instruction for the AI |

### Supported Models (via OpenRouter)

```
anthropic/claude-3.5-sonnet     ← Default (recommended)
anthropic/claude-3-haiku        ← Faster, cheaper
openai/gpt-4o                   ← OpenAI option
google/gemini-pro               ← Google option
meta-llama/llama-3.1-70b        ← Open-source option
```

---

## 🗂 Project Structure

```
finplay-bharat/
│
├── index.html          ← Entire application (single file)
│   │
│   ├── <head>
│   │   ├── Tailwind CDN
│   │   └── Marked.js CDN
│   │
│   ├── <body>
│   │   ├── #loading        → Initial loader overlay
│   │   ├── #app            → Main application wrapper
│   │   │   ├── <aside>     → Sidebar (chat list, controls)
│   │   │   └── <main>      → Chat area (messages + input)
│   │   └── #settingsModal  → Settings overlay
│   │
│   └── <script>  (IIFE)
│       ├── STATE           → In-memory + localStorage state
│       ├── INIT            → Boot logic
│       ├── CHAT MGMT       → Create/switch/save chats
│       ├── RENDER          → Message bubble rendering
│       ├── SEND + STREAM   → API call + SSE handler
│       └── EVENTS          → All DOM event listeners
│
└── README.md
```

---

## 🏗 Architecture Decisions

### ✅ Why Single-File HTML?
- **Zero deployment complexity** — host anywhere (GitHub Pages, S3, local)
- **No build pipeline** — no webpack, no npm, no node_modules
- **Portability** — share as a single file via email/USB

### ✅ Why Vanilla JS (IIFE pattern)?
- No framework overhead
- Full control over DOM
- IIFE (`(function(){...})()`) prevents global namespace pollution

### ✅ Why OpenRouter instead of direct Anthropic API?
- Single API key unlocks 100+ models
- Consistent streaming interface across providers
- Easy model switching without code changes

### ✅ Why localStorage for persistence?
- No backend/database needed
- Instant read/write, zero latency
- Works offline

---

## ⚖️ Pros & Cons Analysis

### 🟢 Strengths

| Aspect | Analysis |
|---|---|
| **Simplicity** | Single HTML file = maximum portability and zero setup friction |
| **Streaming UX** | SSE streaming gives a premium "typing" feel like ChatGPT |
| **Dark Mode** | System-aware toggle improves usability across environments |
| **Model Flexibility** | OpenRouter gateway means you're not locked into one provider |
| **Markdown Support** | `marked.js` properly renders code, tables, and formatting |
| **Responsiveness** | Tailwind utility classes make mobile layout clean and fast |

### 🔴 Limitations & Improvement Areas

| Area | Current Limitation | Suggested Fix |
|---|---|---|
| **API Key Security** | Stored in `localStorage` (plaintext) | Use session-only storage + warn users |
| **Context Window** | Full message history sent every call → costs grow | Add token counting + auto-truncation |
| **Chat Titles** | Always shows "New Chat" | Auto-generate titles from first message |
| **No Export** | Can't export chat history | Add JSON/PDF export button |
| **SSE Error Handling** | Silent `try/catch` on chunk parse | Add visible retry/error states |
| **No Search** | Can't search across chat history | Add in-memory full-text search |
| **Single File Limit** | Hard to scale or add features | Consider modular JS refactor for v2 |

---

## 🗺 Roadmap

```
v1.0  ✅  Core chat + streaming + dark mode + localStorage
v1.1  🔄  Auto-generate chat titles from first message
v1.2  🔲  Export chats (JSON / Markdown)
v1.3  🔲  Token counter + context window warning
v2.0  🔲  PWA support (offline capability)
v2.1  🔲  Multi-language support (Hindi, Gujarati, Tamil...)
v2.2  🔲  Financial data integrations (NSE/BSE live prices)
```

---

## 🤝 Contributing

Contributions are welcome! Here's how:

```bash
# 1. Fork the repo
# 2. Create your branch
git checkout -b feature/your-feature-name

# 3. Make changes to index.html
# 4. Test in multiple browsers

# 5. Submit a PR with description of changes
```

**Please follow these conventions:**
- Keep it single-file (unless proposing v2 architecture)
- Tailwind-only for styling (no custom CSS unless necessary)
- Comment new JS sections clearly

---

## 📄 License

```
MIT License — Free to use, modify, and distribute.
See LICENSE file for details.
```

---

<div align="center">

**Built with ❤️ for Bharat's Financial Community**

*"Empowering every Indian investor with AI-grade analysis"*

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![TailwindCSS](https://img.shields.io/badge/Tailwind-38B2AC?style=flat&logo=tailwind-css&logoColor=white)

</div>
