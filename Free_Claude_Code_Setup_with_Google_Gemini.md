# Free Claude Code Setup Using Google Gemini (Windows)

This guide explains how to use **Claude Code** with **Google Gemini models** for free using **claude-code-router**.

---

## Step 1: Check Node.js Installation

1. Open **PowerShell**
2. Run:

   ```
   node --version
   ```
3. If the version is **18.x or higher**, continue.
4. If not, install **Node.js LTS** from:

   ```
   https://nodejs.org
   ```

---

## Step 2: Create Google Gemini API Key

1. Open:

   ```
   https://aistudio.google.com
   ```
2. Click **Get API Key**
3. Select **Create API Key**
4. Copy the key (starts with `AIzaSy...`)
5. Keep it safe — you'll need it later

---

## Step 3: Install Claude Code & Router

1. Open **PowerShell as Administrator**
2. Run:

   ```
   npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
   ```
3. This installs both tools globally on your system

---

## Step 4: Create Required Folders

Open **normal PowerShell (not admin)** and run:

```
mkdir $HOME/.claude
mkdir $HOME/.claude-code-router
```

These folders store Claude and router settings.

---

## Step 5: Create Router Configuration File

Windows does not support `cat << EOF`, so use **Notepad**.

1. Run:

   ```
   notepad $HOME/.claude-code-router/config.json
   ```
2. Paste **exactly** this configuration:

```json
{
  "LOG": true,
  "LOG_LEVEL": "info",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "API_TIMEOUT_MS": 600000,
  "Providers": [
    {
      "name": "gemini",
      "api_base_url": "https://generativelanguage.googleapis.com/v1beta/models/",
      "api_key": "$GOOGLE_API_KEY",
      "models": [
        "gemini-2.5-flash",
        "gemini-2.0-flash"
      ],
      "transformer": {
        "use": ["gemini"]
      }
    }
  ],
  "Router": {
    "default": "gemini,gemini-2.5-flash",
    "background": "gemini,gemini-2.5-flash",
    "think": "gemini,gemini-2.5-flash",
    "longContext": "gemini,gemini-2.5-flash",
    "longContextThreshold": 60000
  }
}
```

3. Save the file and close Notepad

---

## Step 6: Set Google API Key as Environment Variable

1. Open **PowerShell as Administrator**
2. Run (replace with your key):

   ```
   [System.Environment]::SetEnvironmentVariable(
   'GOOGLE_API_KEY',
   'YOUR_API_KEY_HERE',
   'User'
   )
   ```

### Verify the Key

1. Close PowerShell
2. Open a **new** PowerShell window
3. Run:

   ```
   echo $env:GOOGLE_API_KEY
   ```

If the key shows, it's configured correctly ✅

---

## Step 7: Verify Installation

Run these commands:

```
claude --version
ccr version
echo $env:GOOGLE_API_KEY
```

If all return output without errors, setup is successful 🎉

---

## Step 8: Start Claude Code Router

### Terminal 1

```
ccr start
```

You should see:

```
✔ Service started successfully
```

---

## Step 9: Use Claude Code

### Terminal 2

1. Go to your project folder:

   ```
   cd your-project-folder
   ```
2. Start Claude Code:

   ```
   ccr code
   ```

---

## Step 10: Quick Test

Inside Claude Code, type:

```
hi
```

If Claude replies, your **Claude Code + Google Gemini setup is fully working** ✅🚀

---

### 🎯 Summary

* Claude Code runs locally
* Gemini models are used for free
* Router handles model switching
* Works perfectly on Windows

If you want, I can also:

* Simplify this into **short cheat notes**
* Convert it into a **PDF**
* Or explain **common errors & fixes**

Just tell me 😊