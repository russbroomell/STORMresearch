# STORM Research

## What's in this repo

### [`/storm` — STORM Research Paper Generator](./.claude/commands/storm.md)

A Claude Code slash command that implements the Stanford STORM research method (Synthesis of Topic Outlines through Retrieval and Multi-perspective Question Asking). Type one command, get a PhD-level research paper in minutes.

**Usage:**
```
/storm [your topic]
```

**Example:**
```
/storm the future of nuclear energy in the United States
```

**How it works:**

The command runs 4 phases automatically:

1. **Phase 1 — Multi-Perspective Scan (parallel):** Spins up 5 agents simultaneously, each researching your topic from a different expert lens: The Practitioner, The Academic, The Skeptic, The Economist, and The Historian. All 5 run at the same time.

2. **Phase 2 — Contradiction Map:** Maps where the 5 perspectives clash, ranks the evidence, and surfaces the blind spots no single perspective could find.

3. **Phase 3 — Synthesis:** Compiles everything into a research briefing with an executive summary, 5 key findings ranked by reliability, a hidden cross-perspective insight, and a specific actionable recommendation.

4. **Phase 4 — Peer Review:** Self-critiques the briefing with confidence scores, bias audit, and an overall grade — the step Stanford flagged as missing from the original system.

**Output:** A fully compiled research paper with all four phases, formatted for reading or export to markdown.

**Why parallel agents?** The 5 expert perspectives in Phase 1 are fully independent — there's no reason to run them one at a time. Parallel execution cuts research time dramatically and, more importantly, each agent stays in its own perspective without contaminating the others.

**Based on:** Stanford OVAL Lab's STORM paper, published at NAACL 2024. Peer-reviewed testing showed STORM-generated articles were 25% more organized and 10% broader in coverage than single-prompt research.
