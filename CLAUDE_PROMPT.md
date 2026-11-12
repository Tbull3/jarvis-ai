# Paste this entire block into Claude

You are helping me install and run the Jarvis AI voice assistant on a **Windows 10/11 VM in Parallels** (I'm talking to you from my Mac, but all install/run steps must happen **inside the Windows VM**).

## Goal

Get Jarvis running end-to-end on Windows: clone the repo, install Python 3.10 from python.org, create a venv, install dependencies, create a `.env` with placeholders, put my real Cohere API key in when I paste it, then run `python Main.py` and smoke-test.

## Important constraints

- Use **Windows command syntax only** in the VM: `cd`, `python`, `pip`, `venv\Scripts\activate`. Do **not** use `source`, bash paths like `/workspace`, or macOS commands for the VM steps.
- Install **Python 3.10 from https://www.python.org/downloads/** (recommended 3.10.10). Do **not** use the Microsoft Store Python.
- During install, enable **“Add python.exe to PATH”** and **“pip”**.
- **Ask me for API keys** (Cohere, Groq, Hugging Face, Gemini). Do **not** invent, hardcode, or reuse secrets from chat history unless I paste them in this conversation.
- I already have a Cohere Trial API key. When you create `.env`, use a placeholder for `CohereAPIKey`, then ask me to paste the real key and replace the placeholder.
- `Backend/Automation.py` imports `AppOpener`, which **crashes on non-Windows** with `Exception error: AppOpener only works on windows.` On this Windows VM it should work as-is — do not remove that import unless we hit a different error.

## Repo

Clone into a sensible Windows path, e.g. `%USERPROFILE%\Projects\jarvis-ai` or `C:\Users\<me>\jarvis-ai`:

```bat
git clone https://github.com/Tbull3/jarvis-ai.git
cd jarvis-ai
```

Confirm `Requirements.txt` exists (capital **R**).

## Steps (do these in order inside the Windows VM)

1. **Clone** the repo as above and `cd` into it.
2. **Install Python 3.10** from python.org (not Store). Verify:
   ```bat
   python --version
   pip --version
   ```
   Expect something like `Python 3.10.x`.
3. **Create and activate a venv** in the project root:
   ```bat
   python -m venv .venv
   .venv\Scripts\activate
   ```
4. **Install dependencies**:
   ```bat
   pip install -r Requirements.txt
   ```
   If a package fails, report the exact error and propose a fix before continuing.
5. **Create `.env`** in the project root with placeholders (do not put real keys until I provide them):
   ```env
   # Cohere — intent classification (Backend/Model.py)
   CohereAPIKey=your-cohere-key-here

   # Groq — chat / search / automation content
   GroqAPIKey=your-groq-key-here

   # Hugging Face — image generation
   HuggingFaceAPIKey=your-huggingface-key-here

   # Google Gemini — screen and camera analysis
   GeminiAPIKey=your-gemini-key-here

   # Jarvis identity
   Username=Your Name
   Assistantname=Jarvis
   ```
   Optional speech settings (used by STT/TTS if present):
   ```env
   InputLanguage=en
   AssistantVoice=en-CA-LiamNeural
   ```
   Then **ask me** for:
   - Cohere API key (I already have one — remind me to paste it)
   - Groq API key
   - Hugging Face API key
   - Gemini API key
   - Preferred `Username` / `Assistantname` if I want something other than the defaults

   When I paste keys, update only those fields in `.env`. Never commit `.env` to git.
6. **Run Jarvis**:
   ```bat
   .venv\Scripts\activate
   python Main.py
   ```
7. **Smoke-test** (report what you observe):
   - App window appears (PyQt5 GUI)
   - No immediate crash / traceback
   - Mic / status UI loads
   - If voice works: try a simple spoken or typed-style command path if the UI allows
   - Note: screen/camera analysis needs a real `GeminiAPIKey`; image gen needs Hugging Face; chat/search needs Groq; intent routing needs Cohere

## If something fails

- Paste the full error and the command that caused it.
- If `AppOpener` somehow still errors on Windows, check that you are actually inside the Windows VM (not the Mac host).
- If PyQt or audio fails, check Windows microphone permissions and that Edge / browser dependencies needed for speech are available as described in the project README.

## Success criteria

Jarvis launches on Windows without the Linux `AppOpener only works on windows` crash, `.env` has my real Cohere key (and any other keys I provided), and the GUI is up for a basic smoke test.

Start by confirming you can run commands in the Windows VM, then proceed through the steps. Ask me for the API keys when you reach the `.env` step.
