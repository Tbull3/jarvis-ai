# Jarvis setup

README targets Python 3.10; this machine has 3.12.

```bash
python -m venv .venv
```

```bash
# Linux / macOS
source .venv/bin/activate

# Windows
.venv\Scripts\activate
```

Be in the project root before installing (a "No such file or directory" error means the shell is elsewhere):

```bash
cd /workspace
# or: cd into your jarvis-ai project root
```

```bash
pip install -r Requirements.txt
```

```bash
python Main.py
```
