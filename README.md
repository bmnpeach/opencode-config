# OpenCode Setup — Paste This Into Your Fresh OpenCode Install

## What This Is

This repo contains everything needed to set up your friend's laptop with OpenCode skills, agents, and configuration. Your friend should paste this entire README into their fresh OpenCode session and let the agent do the work.

---

## Your Mission

You are a setup agent configuring a friend's laptop with OpenCode. Your job is to read this README, understand the repo structure, and set up everything on their machine.

**Your friend is a beginner.** They may not have Python, Node.js, git, or anything else installed. Adapt accordingly.

---

## Your Thinking Framework

Before you do anything, internalize these principles:

1. **Assess before acting.** Check what's already installed. Don't install what's already there.
2. **One phase at a time.** Complete each phase before moving to the next.
3. **Verify after each step.** Don't assume success — verify.
4. **Adapt to the environment.** If something fails, find an alternative. Don't give up.
5. **Read the repo's files for instructions.** The repo contains its own setup instructions in each skill's SKILL.md. Use them.
6. **Update your todo list.** Track progress as you go.

---

## Repo Structure

```
opencode-config/
├── README.md              ← You are reading this
├── requirements.txt       ← Python packages to install
├── config-template.json   ← Template for opencode.json (with placeholders)
├── skills/                ← All OpenCode skills
│   ├── brand-storytelling/
│   ├── docx-manipulation/
│   ├── find-skills/
│   ├── opencode-ensemble/
│   ├── pptx-manipulation/
│   ├── ui-ux-pro-max/
│   └── ultrathink/
└── agents/                ← All OpenCode agent files
    └── Ultrathink.md
```

---

## Setup Phases

### Phase 1: Assess the Current State

Check what's already installed. Update your todo list with findings.

**Commands to run:**
```bash
# Check git
which git || echo "git not installed"

# Check Python
python3 --version 2>/dev/null || echo "Python3 not installed"
pip3 --version 2>/dev/null || echo "pip3 not installed"

# Check Node.js
node --version 2>/dev/null || echo "Node.js not installed"
npm --version 2>/dev/null || echo "npm not installed"

# Check OpenCode
which opencode 2>/dev/null || echo "OpenCode not installed"

# Check existing skills directory
ls ~/.agents/skills/ 2>/dev/null || echo "~/.agents/skills/ does not exist"

# Check existing config
cat ~/.config/opencode/opencode.json 2>/dev/null || echo "No opencode.json found"

# Check OS
uname -s
```

**Decision point:** Based on what's installed, determine what needs to be installed first. Create your todo list with phases in order.

---

### Phase 2: Install Prerequisites

Install anything that's missing. For each installation, verify it worked.

**If git is missing:**
- macOS: `brew install git`
- Ubuntu/Debian: `sudo apt install git`
- Fedora: `sudo dnf install git`

**If Python is missing:**
- macOS: `brew install python` or download from python.org
- Ubuntu/Debian: `sudo apt install python3 python3-pip`
- Fedora: `sudo dnf install python3 python3-pip`

**If Node.js is missing:**
- Use nvm: `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash`
- Or download from nodejs.org

**If Homebrew is missing (macOS only):**
- `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

**Verify each installation:**
```bash
git --version
python3 --version
node --version
```

**Decision point:** If the friend already has OpenCode installed, skip to Phase 4. If not, install it:
```bash
npm install -g opencode-ai
```

---

### Phase 3: Clone This Repo

Clone the repo and navigate into it.

```bash
git clone https://github.com/bmnpeach/opencode-config.git
cd opencode-config
```

**Decision point:** If the friend already has this repo cloned, tell them to navigate to it. Don't clone again.

---

### Phase 4: Install Skills

Skills are markdown files that OpenCode reads from the **global skills directory** at `~/.agents/skills/`. Copy each skill directory there.

**Steps:**
1. Create `~/.agents/skills/` if it doesn't exist: `mkdir -p ~/.agents/skills/`
2. Copy each skill from the repo's `skills/` folder to `~/.agents/skills/`
   - Specifically: `skills/ultrathink/SKILL.md` → `~/.agents/skills/ultrathink/SKILL.md`
3. **Do not delete existing skills** — only add yours
4. Verify by listing `~/.agents/skills/`

**Commands:**
```bash
mkdir -p ~/.agents/skills/
cp -r skills/* ~/.agents/skills/
ls ~/.agents/skills/
```

**Read each SKILL.md** to understand what the skill does. Some skills may have additional installation instructions in their README.md.

---

### Phase 5: Install Agents

Agents are markdown files that OpenCode uses as specialized agents. They go into the **global OpenCode config directory** at `~/.config/opencode/agents/`.

**Steps:**
1. Create `~/.config/opencode/agents/` if it doesn't exist: `mkdir -p ~/.config/opencode/agents/`
2. Copy each agent file from the repo's `agents/` folder to `~/.config/opencode/agents/`
   - Specifically: `agents/Ultrathink.md` → `~/.config/opencode/agents/Ultrathink.md`
3. Verify by listing `~/.config/opencode/agents/`

**Commands:**
```bash
mkdir -p ~/.config/opencode/agents/
cp agents/* ~/.config/opencode/agents/
ls ~/.config/opencode/agents/
```

---

### Phase 6: Install Python Packages

Read `requirements.txt` and install the packages.

**Commands:**
```bash
pip3 install -r requirements.txt
```

**Verify each package can be imported:**
```bash
python3 -c "import docx; print('python-docx OK')"
python3 -c "import pptx; print('python-pptx OK')"
python3 -c "import pypdf; print('pypdf OK')"
python3 -c "import openpyxl; print('openpyxl OK')"
```

**Decision point:** If a package import fails, note it but continue. The friend can fix it later.

---

### Phase 7: Configure OpenCode

Read `config-template.json` and help the friend create their `opencode.json`.

**Steps:**
1. Read `config-template.json` to understand the structure
2. Check if the friend already has an `opencode.json`
3. If they do, **merge** the new config rather than overwriting
4. If they don't, create one using the template as a guide
5. **Important:** The friend needs to fill in their own API keys and tokens. Tell them what goes where.

**Key placeholders to explain:**
- `BHARATCODE_API_KEY` — their API key for the BharatCode provider
- `NOTION_TOKEN` — their Notion integration token (they get this from notion.com)
- Any other personal tokens

**Help the friend understand:**
- Where to get each token
- What each config section does
- How to test their configuration after setup

---

### Phase 8: Install External Plugins (Optional)

Some plugins are installed via npm, not copied from the repo. Read the skill's SKILL.md or README.md for instructions.

**Common plugins:**
- `opencode-goal-plugin`: `npm install -g opencode-goal-plugin`
- `opencode-ensemble`: Check the skill's README.md for version-specific instructions

**Decision point:** If the friend doesn't want these plugins, skip them. The skills will still work but some features may be limited.

---

### Phase 9: Final Verification

Before declaring success, verify everything is in place.

**Checklist:**
- [ ] All prerequisites are installed (git, Python, Node.js, OpenCode)
- [ ] All skills are in `~/.agents/skills/`
- [ ] All agents are in `~/.config/opencode/agents/`
- [ ] `opencode.json` exists and is valid JSON
- [ ] All Python packages can be imported
- [ ] OpenCode can start without errors

**Commands to verify:**
```bash
# Check skills
ls ~/.agents/skills/

# Check agents
ls ~/.config/opencode/agents/

# Check Python packages
python3 -c "import docx, pptx, pypdf, openpyxl; print('All OK')"

# Check OpenCode
opencode --version
```

---

### Phase 10: Optional — Wispr Flow + Notion MCP Setup

After the base setup is complete, ask the friend:

> "Do you want to set up Wispr Flow (an AI voice assistant) and Notion MCP integration? These are optional but useful. Wispr Flow lets you talk to OpenCode. Notion MCP lets OpenCode interact with your Notion workspace."

**If they say YES:**

1. **Load the Ultrathink skill** — This is the skill you copied from `skills/ultrathink/SKILL.md`. It's a strategic planning agent that decomposes complex tasks into phases before executing.

2. **Tell Ultrathink to plan it:**
   - Pass the Wispr Flow setup task to the Ultrathink agent
   - Ask it to: assess the friend's OS, determine the correct download link, plan the installation steps, and handle the Notion MCP configuration
   - Ultrathink should break this into phases, identify dependencies, and surface edge cases

3. **What Ultrathink will handle:**
   - **Wispr Flow:**
     - Download from https://wisprflow.ai/downloads
     - Determine the correct installer for the friend's OS (macOS/Windows/Linux, Intel/Apple Silicon)
     - Run the installer
     - Verify it's running
   - **Notion MCP:**
     - Guide the friend to create a Notion integration token at notion.com
     - Add the Notion MCP configuration to their `opencode.json`
     - Test the connection

4. **After Ultrathink plans and executes:**
   - Verify both Wispr Flow and Notion MCP are working
   - Update the friend's `opencode.json` with the Notion token

**If they say NO:**
- Skip to the Final Message section

**Decision point:** If the friend already has Wispr Flow installed, skip the Wispr Flow portion and only set up Notion MCP. If they already have Notion MCP configured, skip that portion.

---

## Edge Cases & Decision Points

| Situation | What to Do |
|-----------|------------|
| Friend already has OpenCode installed | Skip installation, merge config |
| Friend has existing skills | Don't delete them, add yours |
| Friend has existing opencode.json | Merge, don't overwrite |
| Friend is on Linux | Use apt/yum instead of brew |
| Friend is on Windows | Use PowerShell commands |
| Notion token is needed | Tell friend to get it from notion.com |
| A GitHub repo is inaccessible | Skip it, note the issue |
| Python import fails | Note it, continue setup |

---

## Final Message to the Friend

After setup is complete, tell the friend:

1. **Welcome to OpenCode!** Your setup is complete.
2. **Test it out:** Try asking OpenCode to "create a Word document" or "create a PowerPoint"
3. **API keys:** Remind them to fill in their API keys in `opencode.json`
4. **Notion:** If they want Notion integration, they need to create a token at notion.com
5. **Help:** If something doesn't work, they can ask OpenCode to "diagnose my setup"

---

## You're Done When

- All files are in place
- All imports work
- OpenCode can start
- The friend knows what to do next

Don't overthink it. The friend can fix small issues themselves. Your job is to get them to a working state.
