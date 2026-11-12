# Jarvis setup

README targets Python 3.10; this machine has 3.12.

On the Cursor cloud agent VM the project root is `/workspace`. On your Mac that path does not exist — use your local `jarvis-ai` clone instead (for example `~/Projects/jarvis-ai` or wherever you cloned it).

```bash
# Cloud agent:
cd /workspace

# Your Mac (pick the real path to your clone):
# cd ~/path/to/jarvis-ai
```

```bash
# macOS / Linux often need python3 / pip3
python3 -m venv .venv
```

```bash
# Linux / macOS
source .venv/bin/activate

# Windows
.venv\Scripts\activate
```

```bash
# From the project root (file is Requirements.txt with a capital R)
pip3 install -r Requirements.txt

# Or with an absolute path once you know the project root, e.g.:
# pip3 install -r /workspace/Requirements.txt          # cloud agent only
# pip3 install -r ~/path/to/jarvis-ai/Requirements.txt  # Mac
```

```bash
python3 Main.py
```
