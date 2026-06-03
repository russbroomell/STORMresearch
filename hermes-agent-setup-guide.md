# Setting Up a Hermes Agent to Build Your New Business

A step-by-step guide for beginners, based on Matt VanHorn's agentic engineering workflow (June 2026).

---

## What Is a Hermes Agent?

A Hermes agent is a self-learning, autonomous agent ecosystem that runs on your Mac and gets smarter at your repeated business tasks over time. You give it a goal by voice, text, or email — and it researches, plans, and builds, while you direct it like a boss rather than typing like a coder. This guide sets up the full stack: Claude Code as the brain, Compound Engineering for the planning loop, AgentMail so you can email tasks from your phone, and voice so you never have to type much at all.

---

## Before You Start

You need:
- A Mac (M-series chip preferred; M5 Max with 64GB RAM if you want the full setup, but an M1/M2/M3 MacBook will work fine to start)
- An Anthropic account with a Claude Max plan ($200/month) — sign up at claude.ai
- About 2 hours for the initial setup

---

## Part 1: Create a Dedicated Mac User Account

Running your agent on a separate Mac user account keeps it isolated from your personal files and lets it run autonomously without interrupting your main work.

**Step 1: Open System Settings**

1. Click the Apple menu () in the top-left corner of your screen
2. Select **System Settings**
3. Scroll down and click **Users & Groups**

**Step 2: Create a new user**

1. Click the **Add User** button (you may need to click the lock icon and enter your password first)
2. Set **New Account** to **Standard**
3. Fill in:
   - Full Name: `Agent Runner` (or whatever you like)
   - Account Name: `agentrunner` (no spaces, all lowercase)
   - Password: choose a strong password and write it down
4. Click **Create User**

**Step 3: Switch to the new account**

1. Click the Apple menu → **Log Out [your name]**
2. Log in as `agentrunner`

From here, all remaining steps happen inside this new account unless noted otherwise.

---

## Part 2: Install Homebrew (Mac's Package Manager)

Homebrew is a tool that makes installing software on a Mac simple. Almost everything else in this guide uses it.

**Step 1: Open Terminal**

Press `Cmd + Space`, type `Terminal`, and press Enter.

**Step 2: Install Homebrew**

Paste this into Terminal and press Enter:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Follow the prompts. It will ask for your password. This takes 5–10 minutes.

**Step 3: Verify the install**

```bash
brew --version
```

You should see a version number. If you do, Homebrew is installed.

---

## Part 3: Install Claude Code

Claude Code is the AI agent engine at the center of everything.

**Step 1: Install Node.js** (Claude Code requires it)

```bash
brew install node
```

**Step 2: Install Claude Code**

```bash
npm install -g @anthropic-ai/claude-code
```

**Step 3: Log in to Claude Code**

```bash
claude
```

On first run it will open a browser window and ask you to log in with your Anthropic account. Complete the login, then return to Terminal.

---

## Part 4: Configure Claude Code for Autonomous Operation

The default Claude Code asks for permission before every action. For a business agent that runs while you're away, you need it to act without waiting for you.

**Step 1: Open the Claude Code settings file**

```bash
mkdir -p ~/.claude
open -e ~/.claude/settings.json
```

If the file is empty or new, paste in the entire block below. If it already has content, replace it entirely.

**Step 2: Paste this configuration**

```json
{
  "permissions": {
    "allow": [
      "WebSearch",
      "WebFetch",
      "Bash",
      "Read",
      "Write",
      "Edit",
      "Glob",
      "Grep",
      "Task",
      "TodoWrite"
    ],
    "deny": [],
    "defaultMode": "bypassPermissions"
  },
  "skipDangerousModePermissionPrompt": true,
  "remoteControlAtStartup": true,
  "hooks": {
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "afplay /System/Library/Sounds/Blow.aiff"
          }
        ]
      }
    ]
  }
}
```

Save the file (`Cmd + S`) and close it.

**What these settings do:**
- `bypassPermissions` — lets the agent act without asking you each time
- `skipDangerousModePermissionPrompt` — stops the agent from second-guessing itself at startup
- `remoteControlAtStartup` — lets you reach this session from the Claude mobile app on your phone
- The `Stop` hook plays a sound when a task finishes so you hear it across the room

---

## Part 5: Set Your Terminal to Open Directly into Claude Code

A new Terminal tab should drop you straight into your agent, no typing `claude` every time.

**Step 1: Create a launcher script**

```bash
mkdir -p ~/.local/bin
```

Paste this whole block into Terminal and press Enter:

```bash
cat > ~/.local/bin/claude-launcher.sh << 'EOF'
#!/bin/zsh
claude --dangerously-skip-permissions
echo ""
echo "Claude session ended. Dropping into shell."
exec zsh -l
EOF
chmod +x ~/.local/bin/claude-launcher.sh
```

**Step 2: Make Terminal run the launcher automatically**

Open Terminal preferences: `Cmd + ,`

1. Click the **Profiles** tab
2. Select your current profile (usually "Basic")
3. Click the **Shell** tab
4. Check **Run command**
5. Enter: `~/.local/bin/claude-launcher.sh`
6. Uncheck **Run inside shell**
7. Close preferences

Now every new Terminal tab opens straight into Claude Code.

---

## Part 6: Install cmux (Multi-Tab Session Manager)

cmux lets you run 4–6 agent sessions at once, each working on a different business task in parallel.

**Step 1: Install cmux**

```bash
brew install cmux
```

*(If cmux is not available via Homebrew in your version, install tmux instead: `brew install tmux` — it provides the same multi-window capability)*

**Step 2: Start a cmux session**

```bash
cmux new -s business
```

This creates a named session called `business`. Open new windows with `Ctrl+B then C`, and switch between them with `Ctrl+B then [number]`.

**The workflow:** Keep 4–6 windows open at all times:
- One doing research
- One writing a plan
- One building from a finished plan
- One testing or fixing something

---

## Part 7: Install Compound Engineering (The Planning Engine)

Compound Engineering is the plugin that gives Claude Code its `/ce-plan` and `/ce-work` commands — the core of how you'll run every business task.

**Step 1: Open a Claude Code session** (new Terminal tab)

**Step 2: Install the plugin**

Type this inside Claude Code:

```
/plugin marketplace add EveryInc/compound-engineering-plugin
```

Wait for it to install. You should see confirmation that the plugin is active.

**Step 3: Verify it works**

Type `/ce-plan` and press Enter. Claude should respond by asking what you'd like to plan.

---

## Part 8: The Core Business Loop — How to Actually Use This

This is the workflow you will repeat for every business task, large or small.

### Step 1: Research first with last30days

Before making any plan, research what's currently working in your space.

**Install last30days:**

```bash
npm install -g last30days
```

You also need a ScrapeCreators API key (sign up at scrapecreators.com) and set it:

```bash
echo 'export SCRAPECREATORS_API_KEY="your-key-here"' >> ~/.zshrc
source ~/.zshrc
```

**Use it:** Inside Claude Code, type:

```
/last30days [your business topic]
```

Example: `/last30days bootstrapped SaaS pricing models 2026`

This fans out searches across Reddit, X, YouTube, HackerNews, GitHub, and more. Paste or pipe the output into your plan step.

### Step 2: Make a plan

Inside Claude Code:

```
/ce-plan [your goal]
```

Examples:
- `/ce-plan build a waitlist landing page for a meal-kit subscription service`
- `/ce-plan write a competitive analysis for my bookkeeping app idea`
- `/ce-plan create a cold outreach email sequence for B2B sales`

The agent will fan out research agents, read your codebase if you have one, and produce a structured `plan.md` file with: the problem, the approach, what to build, and acceptance criteria.

**Important:** You don't need to read the whole plan. Skim the title. If something looks wrong, ask inline: `why this approach?` or `eli5 this plan`. Then proceed.

### Step 3: Execute the plan

```
/ce-work
```

That's it. The agent picks up the most recent `plan.md` and builds it. Walk away. Come back when you hear the sound.

### Step 4: React and redirect

When it finishes, look at what came back. Your job is to give taste and direction, not to do the work:

- "Option two is closer, but use the language from option one"
- "Address the biggest risk first"
- "This is too long, cut it in half"

Then run `/ce-work` again.

---

## Part 9: Set Up Voice Input (So You Never Have to Type Much)

Voice-to-LLM works better than voice-to-anything-else because the model fills in what the mic gets wrong. You can mumble and trail off.

**On Mac:**

Install **Monologue** (from Every.io) or **Wispr Flow**:

- Monologue: monologue.so
- Wispr Flow: wisprflow.com

Pick one. Both pipe speech directly into whatever app is in focus. Click into your Terminal window with Claude Code open, start talking, and your words appear as text input.

**Recommended:** Buy a gooseneck desk mic. The built-in mic works, but a dedicated mic reduces errors and is more comfortable for long sessions.

**On iPhone:**

Use Apple's built-in dictation (press the microphone key on the keyboard). It's good enough because you're talking to an LLM, not a human — it can mangle words and the agent still gets it.

---

## Part 10: Give Your Agent an Email Address (Send Tasks From Anywhere)

This is how you run tasks from your phone without SSH or VPN. Email a task from the soccer field, and a Claude session opens on your Mac and starts working.

**Step 1: Sign up for AgentMail**

Go to agentmail.to and create an account. Create a new inbox — save the inbox address and your API key.

**Step 2: Clone and set up the integration**

Inside Terminal (not inside Claude Code):

```bash
git clone https://github.com/mvanhorn/agentmail-to-claude-code
cd agentmail-to-claude-code
```

**Step 3: Configure the environment**

```bash
cp cc.env.example cc.env
open -e cc.env
```

Fill in:
- `AGENTMAIL_API_KEY` — your AgentMail API key
- `AGENTMAIL_INBOX` — your inbox address
- `ALLOWLIST` — your personal email addresses only (comma-separated). Only these addresses can trigger the agent.
- `TERMINAL` — set to `cmux` or `ghostty` depending on what you installed

**Step 4: Run the daemon and install it to run on startup**

Inside your Claude Code session, paste:

```
Give Claude Code an email address using the agentmail-to-claude-code repo I just cloned. Run the daemon and install it as a launchd job so it starts automatically when I log in.
```

The daemon watches your AgentMail inbox over WebSocket. When an email arrives from an allowlisted address, it opens a fresh Claude session and runs the task from the email subject and body.

**Step 5: Test it**

From your phone, send an email to your AgentMail inbox with:
- Subject: `Research pricing for a subscription app`
- Body: `Look at what B2B SaaS apps charge per seat in 2026 and summarize the range for a solo founder.`

Within seconds, a Claude session should open on your Mac and start working.

---

## Part 11: Set Up Your Notes as the Agent's Knowledge Base

The more context your agent has about your business, the better every plan gets. Point it at your notes.

**Option A: Bear (if you use Bear for notes)**

Install the Bear CLI:

```bash
brew install bear-cli
```

Inside Claude Code, you can now ask it to search your notes:

```
Search my Bear notes for anything about [business topic]
```

**Option B: Obsidian**

If you use Obsidian, install the Obsidian CLI plugin (community plugins → search "CLI") and point Claude at your vault directory. Inside a Claude session:

```
My Obsidian vault is at ~/Documents/MyVault. When planning, search it for relevant notes.
```

**Make it a habit:** After every business meeting, customer call, or idea session, write a quick note. The agent reads everything you've written and gets smarter every time.

---

## Part 12: Business-Specific Workflows

### Analyzing a business idea

```
/ce-plan make a plan for the plan. I have a business idea I want to stress-test.
Here is my idea: [describe your idea in plain language]
I want a plan for how you'll research the market, find comparable products, identify the biggest risks, and produce a one-page assessment I could show a smart friend.
Do not write the assessment yet. Only plan how you'll produce it.
```

Then: `/ce-work`

### Turning a meeting transcript into a strategy doc

Record your meeting with Granola (granola.ai). After, paste the raw transcript into Claude Code:

```
/ce-plan Here is a raw transcript from a meeting I just had about [topic].
[paste full transcript]
Turn this into a structured strategy document. Do not summarize the transcript first — extract what matters directly.
```

### Competitive research

```
/last30days [competitor name] reviews 2026
```

Then pipe the output into a plan:

```
/ce-plan Here is fresh research on [competitor]. 
[paste last30days output]
Write me a one-page competitive positioning doc: where they're weak, where we could win, what features customers are asking for that they don't have.
```

### Writing cold outreach

```
/ce-plan write a five-email cold outreach sequence for [target customer type].
Context: my product is [one sentence description], the pain point is [one sentence], the proof point is [one sentence].
Research what's currently working in cold email before writing anything.
```

### Writing a weekly business update

```
/ce-plan review my recent Bear/Obsidian notes and any plan.md files from this week, and draft a weekly business update covering: what we shipped, what we learned, what's next, and the biggest open question.
```

---

## Part 13: Keeping Your Agent Healthy

**Prevent your Mac from sleeping while the agent runs:**

```bash
sudo pmset -a disablesleep 1
```

Enter this in Terminal (not inside Claude Code). It needs your password.

**Check that remote control is working:**

Download the Claude app on your iPhone. Your Mac sessions should appear in the "Remote" section. You can view, steer, and redirect any running session from your phone.

**Back up your plans:**

All `plan.md` files are your checkpoints. If a session crashes or runs out of context, start a new session and point it at the plan:

```
Read plan.md and pick up where we left off.
```

The plan survives everything. That's the point.

---

## Quick Reference Card

| Goal | Command |
|------|---------|
| Research a topic | `/last30days [topic]` |
| Make a plan | `/ce-plan [goal]` |
| Execute the plan | `/ce-work` |
| Fuzzy idea, not sure where to start | `/ce-brainstorm` first, then `/ce-plan` |
| Deep doc (meeting, book, transcript) | `/ce-plan make a plan for the plan` |
| Ask about the plan without reading it | `eli5 this plan` or `tldr?` |
| Send a task from your phone | Email your AgentMail inbox |

---

## The Mindset Shift

When you run multiple agents, your job is not to do the work. Your job is to be the signal.

The agents supply volume. You supply taste, direction, and the react-and-redirect loop. The rare, valuable thing in the loop is your judgment — not your typing. You look at what came back and say "option two is closer but use the language from option one," and they move.

Be the taste. Let them be the hands.

---

## Troubleshooting

**Claude asks for permission even after I set bypassPermissions**

Make sure the `settings.json` is in `~/.claude/settings.json` (the home directory of the `agentrunner` user, not your main user). Open a new Terminal tab after saving the file.

**I don't hear the completion sound**

The sound file path `/System/Library/Sounds/Blow.aiff` exists on macOS 13+. If you're on an older version, try `/System/Library/Sounds/Glass.aiff`.

**AgentMail daemon isn't starting**

Check that your `cc.env` file has no extra spaces around the `=` signs. Each line should look like `KEY=value` with nothing else.

**The agent runs out of context mid-task**

Start a new session and say: `Read plan.md and pick up where we left off.` The plan is the checkpoint.

**Voice input is too inaccurate**

Make sure the app (Monologue or Wispr Flow) has microphone access: System Settings → Privacy & Security → Microphone.
