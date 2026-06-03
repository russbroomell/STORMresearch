# scaling-pancake

Resources for setting up an autonomous agent ecosystem on a Mac to help build a new business, based on Matt VanHorn's agentic engineering workflow (June 2026).

## What's in this repo

### [`hermes-agent-setup-guide.md`](./hermes-agent-setup-guide.md)

A complete beginner's guide to setting up a Hermes agent — a self-learning, autonomous Claude Code ecosystem that gets smarter at your repeated business tasks over time. Assumes you can set up a Mac but have no prior experience with AI agents or the terminal.

**Covers:**
- Creating a dedicated Mac user account to run the agent autonomously
- Installing and configuring Claude Code with full autonomous permissions
- Setting up Compound Engineering (`/ce-plan` + `/ce-work`) for the research-plan-build loop
- Configuring voice input so you can direct the agent by talking
- Giving the agent an email address so you can send tasks from your phone
- Connecting your notes (Bear, Obsidian) as the agent's knowledge base
- Keeping 4–6 parallel agent sessions running with cmux
- Business-specific workflows: idea analysis, competitive research, meeting transcripts, cold outreach, weekly updates

## The core idea

Traditional work is 80% doing, 20% thinking. This stack flips it. You provide taste and direction; the agents provide volume and execution. Every task follows the same loop:

1. **Research** with `/last30days [topic]`
2. **Plan** with `/ce-plan [goal]`
3. **Build** with `/ce-work`
4. **React and redirect**
