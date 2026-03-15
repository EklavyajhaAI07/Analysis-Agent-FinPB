# FinPlay Bharat Analysis Engine 🚀

A **production-grade AI chat interface** inspired by ChatGPT/Claude, built with **zero build tools** using vanilla JavaScript, Tailwind CSS, and OpenRouter API.

> **One single `index.html` file. Copy. Paste. Run. Done.**

---

## ✨ Features

### Core Functionality
- 💬 **Real-time AI Chat** - Stream responses token-by-token from OpenRouter API
- 🔐 **Secure API Integration** - OpenRouter support with configurable API keys
- 💾 **Chat Persistence** - All conversations saved to browser localStorage
- 🎨 **Dark Mode** - Toggle dark/light theme with persistent preference

### Advanced Features
- 📁 **Chat Management**
  - Create unlimited chats
  - Rename chats on-the-fly
  - Delete individual conversations
  - Chat history sidebar with active indicator

- ⌨️ **Smart Input**
  - Auto-resizing textarea (grows with text)
  - Keyboard shortcuts (Shift+Enter for multiline)
  - Auto-focus after send

- 🧠 **System Prompts**
  - Define custom AI behavior per chat
  - Global system prompt settings
  - Persistent across sessions

- 📱 **Mobile First**
  - Fully responsive design
  - Hamburger sidebar toggle
  - Input bar always visible (no keyboard hiding)
  - Touch-friendly buttons

- 🎯 **Developer Experience**
  - **Zero dependencies** - CDN libraries only
  - **No build step** - Works immediately
  - **Vanilla JavaScript** - Pure ES6+
  - **Clean code** - Modular, well-commented
  - **Safe by default** - DOMPurify sanitization

### UX Enhancements
- ✍️ **Typing Animation** - Letter-by-letter cursor animation
- 📊 **Markdown Rendering** - Full markdown support with code highlighting
- 🛡️ **Error Handling** - Defensive checks, user-friendly error messages
- ⏳ **Loading States** - Disabled send button during streaming
- 📍 **Auto-scroll** - Messages auto-scroll to latest

---

## 🎯 Quick Start

### Step 1: Get Your Files
Download `index.html` from the repository or copy the code directly.

### Step 2: Get OpenRouter API Key
1. Visit [openrouter.ai](https://openrouter.ai)
2. Sign up (free tier available)
3. Generate API key
4. Copy the key (format: `sk-or-v1-...`)

### Step 3: Open & Configure
```bash
# Simply open index.html in your browser
# No installation needed!

# On Mac:
open index.html

# On Windows:
start index.html

# Or drag & drop into browser
```

### Step 4: Add Your Settings
1. Click **⚙️ Settings** in sidebar
2. Paste API Key in "OpenRouter API Key" field
3. Set Model (e.g., `openai/gpt-3.5-turbo`)
4. (Optional) Add System Prompt for custom AI behavior
5. Click **Save Settings**

### Step 5: Start Chatting! 🎉
- Type your message in the input box
- Press **Enter** to send (or click Send button)
- Watch responses stream in real-time
- Create new chats with **+ New Chat**

---

## 🏗️ Architecture Overview

### Single File, Modular Structure

```
index.html (1006 lines)
├── HEAD
│   ├── Meta tags (viewport, charset)
│   ├── CDN libraries
│   │   ├── Tailwind CSS
│   │   ├── Marked.js (Markdown)
│   │   └── DOMPurify (Security)
│   └── Custom CSS
│       ├── CSS Variables (theming)
│       ├── Component styles
│       └── Responsive breakpoints
│
├── BODY (HTML)
│   ├── Loading fallback
│   ├── Main app container
│   ├── Sidebar (chat history)
│   ├── Chat area (messages + input)
│   ├── Settings modal
│   └── Rename modal
│
└── SCRIPT (JavaScript)
    ├── State Management (store object)
    ├── DOM References (cached selectors)
    ├── UI Rendering (render functions)
    ├── Chat Functions (send, switch, etc)
    ├── Event Listeners (all interactions)
    └── Initialization (setup on load)
```

### State Management

```javascript
const store = {
  chats: {},           // { chat_id: { id, title, messages, createdAt } }
  currentChatId: null, // Active chat ID
  apiKey: '',          // OpenRouter API key
  model: '',           // Selected model
  systemPrompt: '',    // Global system prompt
  isDarkMode: false    // Theme preference
}
```

### Data Flow

```
User Input
    ↓
sendMessage() function
    ↓
Add user message to store
    ↓
Fetch from OpenRouter API (streaming)
    ↓
Parse SSE response (token by token)
    ↓
Update bubble innerHTML with markdown
    ↓
Save full response to store
    ↓
Render UI
```

---

## ⚙️ Configuration

### Default Settings

| Setting | Default | Where to Change |
|---------|---------|-----------------|
| Model | `openai/gpt-3.5-turbo` | Settings modal |
| API Key | Empty | Settings modal |
| System Prompt | Empty | Settings modal |
| Dark Mode | False | Theme toggle button |
| Max textarea height | 150px | CSS line 145 |
| Max messages per chat | Unlimited | N/A |

### Change Default Values

**Edit Default Model (line ~480):**
```javascript
model: localStorage.getItem('model') || 'openai/gpt-4-turbo'
```

**Edit App Name (line ~48):**
```html
<h1 class="text-lg font-bold">Your App Name</h1>
```

**Change Primary Color (line ~25):**
```css
--accent-color: #ff6b6b; /* Your color instead of #10a37f */
```

**Add Custom System Prompt:**
```javascript
systemPrompt: localStorage.getItem('systemPrompt') || 'You are a helpful AI assistant.'
```

---

## 🌐 Available Models

OpenRouter supports 100+ models. Popular options:

| Model | Speed | Cost | Quality |
|-------|-------|------|---------|
| `openai/gpt-3.5-turbo` | ⚡⚡⚡ | 💰 | ⭐⭐⭐ |
| `openai/gpt-4` | ⚡⚡ | 💰💰💰 | ⭐⭐⭐⭐⭐ |
| `openai/gpt-4-turbo` | ⚡⚡ | 💰💰 | ⭐⭐⭐⭐⭐ |
| `anthropic/claude-3-sonnet` | ⚡⚡ | 💰💰 | ⭐⭐⭐⭐ |
| `meta-llama/llama-2-70b-chat` | ⚡⚡ | 💰 | ⭐⭐⭐ |
| `mistralai/mistral-7b-instruct` | ⚡⚡⚡ | 💰 | ⭐⭐⭐ |

See full list: [OpenRouter Models](https://openrouter.ai/models)

---

## 📱 Mobile Responsiveness

### Tested On:
- ✅ iPhone 12/13/14/15
- ✅ Android Chrome (latest)
- ✅ iPad (portrait & landscape)
- ✅ Desktop (Chrome, Firefox, Safari, Edge)

### Mobile Features:
- Hamburger menu (☰) toggles sidebar
- Overlay backdrop closes sidebar
- Input bar sticky at bottom
- Messages adjust to 90% width
- Touch-friendly button sizes

### Breakpoints:
```css
/* Mobile (< 768px) */
- Sidebar: Fixed position, off-screen by default
- Hamburger: Visible
- Layout: Single column

/* Desktop (≥ 768px) */
- Sidebar: Always visible
- Hamburger: Hidden
- Layout: Sidebar + Main area
```

---

## 🔒 Security

### Security Features Implemented:

1. **DOMPurify Integration**
   - Sanitizes markdown output
   - Prevents XSS attacks
   - Removes malicious scripts

2. **API Key Handling**
   - Stored in browser localStorage (same as browser history)
   - Sent to OpenRouter via HTTPS only
   - Never logged or transmitted elsewhere
   - ⚠️ For production: Use backend proxy to hide API key

3. **Input Validation**
   - Checks for empty messages
   - Validates API key presence
   - Error boundaries in try-catch blocks

4. **Markdown Rendering**
   - Uses marked.js library (battle-tested)
   - HTML is sanitized before rendering
   - No execution of arbitrary code

### Security Best Practices:
```javascript
// ✅ Safe: Uses DOMPurify + marked.js
bubble.innerHTML = DOMPurify.sanitize(marked.parse(content));

// ❌ Unsafe: Would be vulnerable to XSS
bubble.innerHTML = content;
```

---

## 📂 File Structure

```
FinPlay-Bharat-Analysis-Engine/
├── index.html                 # Main application file (1006 lines)
├── README.md                  # This file
└── (No other files needed!)
```

---

## 🚀 Deployment Options

### Option 1: GitHub Pages (Recommended)

```bash
# 1. Create GitHub repository
# 2. Upload index.html to repo root
# 3. Go to Settings → Pages
# 4. Select "Deploy from branch" → main
# 5. Access at: https://yourusername.github.io/repo-name

# Free, fast, automatic HTTPS ✅
```

### Option 2: Netlify

```bash
# 1. Drag & drop index.html to netlify.com
# 2. Or connect GitHub repo for auto-deploy
# 3. Automatic HTTPS & CDN ✅
```

### Option 3: Vercel

```bash
# 1. Create project at vercel.com
# 2. Upload index.html
# 3. Auto-deployed with HTTPS ✅
```

### Option 4: Local Server

```bash
# Simple HTTP server
python -m http.server 8000
# Or: npx http-server
# Access at: http://localhost:8000
```

### Option 5: Self-Hosted

```bash
# Any web server works (Apache, Nginx, etc.)
# Just serve index.html as static file
# Supports HTTPS with Let's Encrypt
```

---

## 🛠️ Customization Guide

### Change App Theme

**Accent Color:**
```css
:root {
    --accent-color: #10a37f;  /* Change this line */
}
```

**Dark Mode Colors:**
```css
html.dark-mode {
    --bg-primary: #1a1a1a;    /* Change these */
    --bg-secondary: #2a2a2a;
}
```

### Modify UI Text

**Placeholder text:**
```html
<textarea placeholder="Ask FinPlay Bharat anything...">
<!-- Change "Ask FinPlay Bharat anything..." -->
```

**App name in sidebar:**
```html
<h1>FinPlay Bharat</h1>
<p>Analysis Engine</p>
```

### Add Custom Models List

Add a dropdown instead of text input:
```html
<select id="modelInput" class="settings-input">
    <option value="openai/gpt-4">GPT-4</option>
    <option value="openai/gpt-3.5-turbo">GPT-3.5</option>
    <option value="anthropic/claude-3-sonnet">Claude 3</option>
</select>
```

### Increase Input Textarea Height

**Line 145 in CSS:**
```css
.input-field {
    max-height: 300px;  /* Change from 150px */
}
```

---

## 🐛 Troubleshooting

### Issue: Blank Page on Load

**Solution:**
- Check browser console (F12) for errors
- Ensure all CDN libraries loaded (check Network tab)
- Try hard refresh (Ctrl+Shift+R or Cmd+Shift+R)

### Issue: API Key Not Saving

**Solution:**
- Check if localStorage is enabled in browser
- Try incognito/private mode first
- Clear browser cache and try again
- Check if you're in an iframe (localStorage disabled)

### Issue: Streaming Not Working

**Solution:**
- Verify API key is correct (copy from openrouter.ai)
- Check if model name is valid: [openrouter.ai/models](https://openrouter.ai/models)
- Ensure you have API credit balance
- Check OpenRouter status page for outages

### Issue: Messages Not Appearing

**Solution:**
- Check browser console for JavaScript errors
- Verify API key and model in settings
- Try with a shorter message first
- Clear localStorage: `localStorage.clear()` in console

### Issue: Mobile Sidebar Not Closing

**Solution:**
- Click overlay (gray area) to close
- Swipe back on iOS
- Refresh page if stuck
- Try different browser

### Issue: Dark Mode Not Persisting

**Solution:**
- Check if localStorage is enabled
- Try in non-private/non-incognito mode
- Clear cookies and try again

---

## 📊 Storage & Limits

### localStorage Capacity

| Browser | Limit | Reality |
|---------|-------|---------|
| Chrome | 10MB | ~10MB per origin |
| Firefox | 10MB | ~10MB per origin |
| Safari | 5MB | ~5MB per origin |
| Edge | 10MB | ~10MB per origin |

**For FinPlay:**
- Average chat: ~5KB
- 100 chats: ~500KB
- 1000 chats: ~5MB
- Settings: ~1KB

✅ **You can store 100+ full conversations easily**

### How to Clear Storage

```javascript
// In browser console (F12):
localStorage.clear()  // Clears all data
localStorage.removeItem('chats')  // Clears only chats
localStorage.removeItem('apiKey')  // Clears only API key
```

---

## 🎓 Learning Resources

### Understanding the Code

**For Beginners:**
1. Read the HTML structure (lines 230-590)
2. Understand CSS variables (lines 18-40)
3. Learn basic JavaScript (lines 600-650)

**For Intermediate:**
1. Study state management pattern (lines 605-700)
2. Understand event listeners (lines 913-950)
3. Learn DOM manipulation (lines 730-750)

**For Advanced:**
1. Study streaming response parsing (lines 822-850)
2. Understand async/await (lines 761-865)
3. Learn fetch API and ReadableStream

### Suggested Improvements to Learn

1. **Add Image Upload** - Use OpenRouter vision API
2. **Export Chat as PDF** - Use jsPDF library
3. **Search Past Chats** - Filter by keywords
4. **Voice Input** - Use Web Speech API
5. **Conversation Branching** - Fork chats at any message
6. **Model Comparison** - Run same prompt on 2 models
7. **Rate Limiting** - Throttle API calls
8. **Caching** - Store similar responses

---

## 🤝 Contributing

This is a single-file educational project. To contribute:

1. Fork the repository
2. Make improvements
3. Test thoroughly on mobile & desktop
4. Submit a pull request with description
5. Include before/after screenshots if UI changes

---

## 📝 License

This project is **MIT Licensed** - free for personal and commercial use.

```
MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.
```

---

## 💡 Pro Tips

### Tip 1: Save Your API Key Securely
```
✅ Use password manager to store API key
❌ Don't share screenshots showing API key
✅ Rotate key monthly in OpenRouter dashboard
```

### Tip 2: Optimize for Your Use Case
```javascript
// For Indian market analysis:
systemPrompt: "You are an expert in Indian finance and markets. 
Provide analysis in English/Hindi with context for Indian audience."
```

### Tip 3: Bulk Import Chats
```javascript
// Paste in console to import from other ChatGPT exports:
localStorage.setItem('chats', JSON.stringify(importedChats))
```

### Tip 4: Monitor API Usage
- Check OpenRouter dashboard for costs
- Set spending limits
- Use cheaper models for testing

### Tip 5: Backup Your Chats
```javascript
// Copy & save this in text file:
JSON.stringify(JSON.parse(localStorage.getItem('chats')), null, 2)
```

---

## 🔗 Useful Links

- **OpenRouter Docs**: https://openrouter.ai/docs
- **Marked.js**: https://marked.js.org/
- **DOMPurify**: https://github.com/cure53/DOMPurify
- **Tailwind CSS**: https://tailwindcss.com/
- **MDN Web Docs**: https://developer.mozilla.org/

---

## 📞 Support

### Getting Help

1. **Check Troubleshooting section** above
2. **Read code comments** in index.html
3. **Check browser console** (F12) for errors
4. **Search similar issues** on GitHub
5. **Create an issue** with error logs

### Reporting Bugs

When reporting issues, include:
- ✅ Browser & version (Chrome 120, Safari 17, etc.)
- ✅ Device type (iPhone, Android, Desktop)
- ✅ Steps to reproduce
- ✅ Error message from console
- ✅ Screenshots if visual issue

---

## 🎉 Success Checklist

After setup, verify:

- [ ] index.html opens in browser
- [ ] No blank page (wait 2-3 seconds)
- [ ] Settings button works
- [ ] API key saves successfully
- [ ] Can send a message
- [ ] Response streams in real-time
- [ ] Dark mode toggle works
- [ ] New chat button creates chat
- [ ] Rename chat works
- [ ] Delete chat works
- [ ] Works on mobile (resize browser)
- [ ] Messages persist after refresh

✅ All checked? **You're ready to go!** 🚀

---

## 🌟 Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | Mar 2026 | Initial release |

---

## 🙏 Credits

**Built with:**
- Vanilla JavaScript (ES6+)
- Tailwind CSS
- Marked.js
- DOMPurify
- OpenRouter API

**Inspired by:**
- ChatGPT UI
- Claude.ai
- Modern web standards

---

## 📈 Future Roadmap

Potential features for future versions:

- [ ] Local LLM support (Ollama)
- [ ] Multiple API provider support
- [ ] Voice input/output
- [ ] Image generation integration
- [ ] Chat export to PDF/Word
- [ ] Conversation branching
- [ ] Collaborative chats (shared links)
- [ ] Plugin system
- [ ] Custom themes marketplace
- [ ] Analytics dashboard

---

## 🎯 Final Notes

**Remember:**
- This is a **demo/educational project**
- For production, add **backend proxy** for API keys
- Test on **your target devices** before deploying
- Monitor **OpenRouter billing** regularly
- **Backup important chats** locally
- Keep **dependencies updated** (CDN libraries)

**Questions?** Check the code comments - they explain everything! 💬

---

## 🚀 Happy Coding!

```
        _______________
       /               \
      |  FinPlay Bharat |
      | Analysis Engine |
       \_______________/
             |||
             vvv
      Let's Build Something Amazing!
```

**Last Updated:** March 2026  
**Maintained By:** FinPlay Development Team  
**License:** MIT  

---

*Made with ❤️ for the Indian AI community*
