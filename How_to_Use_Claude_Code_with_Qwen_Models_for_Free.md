# Use Claude Code with Qwen Models (Free Setup Guide)

This guide explains how to connect **Claude Code** with **Qwen coding models** using **Claude Code Router**, without paid APIs.

---

## ✅ What You Need Before Starting

Make sure these are already installed:

* **Node.js 18 or newer**

  ```
  node --version
  ```
* **Qwen Code CLI**
* Qwen CLI must be **logged in and authenticated**

---

## 🔹 Install Qwen Code CLI

Open terminal (PowerShell / WSL) and run:

```bash
npm install -g @qwen-code/qwen-code@latest
```

Check installation:

```bash
qwen --version
```

If the version shows, Qwen CLI is ready ✅

---

## 🔹 Install Claude Code & Router

Install both tools globally:

```bash
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
```

These tools allow Claude Code to talk to external models like Qwen.

---

## 🔐 Get Your Qwen Access Token

After logging in with Qwen CLI, go to:

```
C:\Users\YOUR_USERNAME\.qwen\oauth_creds.json
```

Open the file and copy the value of:

```json
"access_token"
```

⚠️ This token expires — you may need to refresh it later.

---

## 📂 Create Claude Configuration Folders

Run these commands (WSL or PowerShell):

```bash
mkdir -p ~/.claude
mkdir -p ~/.claude-code-router
```

These folders store Claude and router settings.

---

## ⚙️ Create Router Config File

### WSL / Linux Terminal

Create the config file:

```bash
cat > ~/.claude-code-router/config.json << 'EOF'
{
  "LOG": true,
  "LOG_LEVEL": "info",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "API_TIMEOUT_MS": 600000,
  "Providers": [
    {
      "name": "qwen",
      "api_base_url": "https://portal.qwen.ai/v1/chat/completions",
      "api_key": "YOUR_QWEN_ACCESS_TOKEN_HERE",
      "models": [
        "qwen3-coder-plus"
      ]
    }
  ],
  "Router": {
    "default": "qwen,qwen3-coder-plus",
    "background": "qwen,qwen3-coder-plus",
    "think": "qwen,qwen3-coder-plus",
    "longContext": "qwen,qwen3-coder-plus",
    "longContextThreshold": 60000,
    "webSearch": "qwen,qwen3-coder-plus"
  }
}
EOF
```

🔁 Replace `YOUR_QWEN_ACCESS_TOKEN_HERE` with your copied token.

---

## ▶️ Start Claude Code with Qwen

Restart the router:

```bash
ccr restart
```

Launch Claude Code:

```bash
ccr code
```

Test it:

```
hi
```

If Qwen replies, the setup is working 🎉

---

## 🔄 Fixing 401 / Token Expired Errors

Qwen tokens **expire frequently**. If you see **401 Unauthorized**:

### Step 1: Re-login to Qwen

Delete old credentials:

```bash
rm ~/.qwen/oauth_creds.json
```

Login again:

```bash
qwen
```

---

### Step 2: Update Router Config

Open config file:

```powershell
notepad "$env:USERPROFILE\.claude-code-router\config.json"
```

Replace the old `api_key` with the new `access_token`.

---

### Step 3: Restart Router

```bash
ccr restart
```

---

## 🧠 Key Notes

* Qwen OAuth tokens are **temporary**
* Router must be restarted after token changes
* Config file must be **valid JSON**
* Claude Code itself is just the interface

---

## ✅ Final Result

You now have:

* Claude Code UI
* Qwen coding models
* Free local workflow
* No paid API required

---

If you want, I can also:

* Convert this into **short cheat notes**
* Make a **Windows-only version**
* Explain **Qwen vs Gemini vs Claude**
* Help debug **router errors**

Just tell me 😊