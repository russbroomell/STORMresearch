# STORM Research Paper Generator

You are executing the Stanford STORM research method (Synthesis of Topic Outlines through Retrieval and Multi-perspective Question Asking) on the following topic:

**Topic: $ARGUMENTS**

If no topic was provided, ask the user: "What topic would you like me to research using the STORM method?"

---

## Your Job

Produce a full, structured research paper on the topic by running all four STORM phases. Phases 1 runs in **parallel** (5 agents at once). Phases 2–4 run **sequentially**, each building on the last. Compile the final paper at the end.

Do not ask clarifying questions. Start immediately.

---

## Phase 1 — Multi-Perspective Scan (PARALLEL)

Spawn exactly **5 agents simultaneously** in a **single message** using the Agent tool. Each agent researches the topic from one expert lens. Pass the topic explicitly in each agent's prompt.

Run these 5 agents in parallel right now:

**Agent 1 — The Practitioner**
Prompt:
```
You are THE PRACTITIONER. Research the following topic from the perspective of someone who works with it every day: "$ARGUMENTS"

Provide:
1. CORE POSITION (2 sentences): What is the practitioner's fundamental view of this topic?
2. STRONGEST EVIDENCE: What real-world observations, case studies, or hands-on data support their view?
3. INSIDER KNOWLEDGE: The one thing a practitioner would tell someone that no academic or theorist would know — a practical reality that textbooks miss.
4. COMMON MISCONCEPTIONS: What do outsiders get wrong about this topic that practitioners find frustrating?
5. WHAT ACTUALLY WORKS: Specific practices, tools, or approaches that produce results in the real world.

Be concrete and specific. Avoid generic statements. Write as if you are briefing a smart person who has never worked directly in this field.
```

**Agent 2 — The Academic**
Prompt:
```
You are THE ACADEMIC. Research the following topic from the perspective of a scholar who has spent years studying it rigorously: "$ARGUMENTS"

Provide:
1. CORE POSITION (2 sentences): What does the peer-reviewed evidence actually conclude about this topic?
2. STRONGEST EVIDENCE: What studies, meta-analyses, or scholarly consensus support the academic view?
3. WHERE EVIDENCE CONTRADICTS POPULAR BELIEF: What does rigorous research show that surprises most people?
4. OPEN QUESTIONS: What does the academic community still genuinely not know or debate?
5. METHODOLOGICAL CAVEATS: What are the limits of the current research — what can't we conclude yet?

Cite specific types of research (randomized trials, longitudinal studies, meta-analyses, etc.) even if you cannot name specific papers. Be precise about what the evidence does and does not support.
```

**Agent 3 — The Skeptic**
Prompt:
```
You are THE SKEPTIC. Research the following topic from the perspective of someone who believes the mainstream view is wrong or overstated: "$ARGUMENTS"

Provide:
1. CORE POSITION (2 sentences): What is the skeptic's fundamental challenge to the mainstream view?
2. STRONGEST EVIDENCE: What data, arguments, or examples support the skeptical position?
3. THE IGNORED EVIDENCE: What facts or findings do proponents of the mainstream view conveniently downplay or ignore?
4. THE STEELMAN: What is the most charitable version of the mainstream view — and why does even that fall short?
5. WHAT WOULD CHANGE MY MIND: What evidence, if it existed, would convince the skeptic they were wrong?

Be intellectually rigorous. This is not cynicism — it is the strongest possible challenge to the consensus. Identify real weaknesses, not strawmen.
```

**Agent 4 — The Economist**
Prompt:
```
You are THE ECONOMIST. Research the following topic through the lens of incentives, money, and structural interests: "$ARGUMENTS"

Provide:
1. CORE POSITION (2 sentences): How do financial incentives and power structures shape how this topic is understood and presented?
2. WHO PROFITS: Which industries, institutions, or individuals benefit most from the current narrative around this topic?
3. FOLLOW THE MONEY: How do funding sources, market structures, or economic incentives influence the research, media coverage, or policy around this topic?
4. MISALIGNED INCENTIVES: Where do the incentives of experts, institutions, or advocates diverge from what is actually best for the public or end user?
5. THE COUNTERFACTUAL: What would the field look like if the dominant financial incentives were removed or reversed?

Be specific about mechanisms, not just vague claims about "money in the system." Name the structural forces at work.
```

**Agent 5 — The Historian**
Prompt:
```
You are THE HISTORIAN. Research the following topic by looking for patterns across time and parallel cases in history: "$ARGUMENTS"

Provide:
1. CORE POSITION (2 sentences): What historical patterns or precedents are most relevant to understanding this topic?
2. THE CLOSEST PARALLEL: What historical situation most resembles the current state of this topic — and how did it play out?
3. WHAT HISTORY PREDICTS: Based on how similar situations have unfolded before, what is the most likely trajectory for this topic?
4. THE LESSON PEOPLE IGNORE: What historical lesson is directly applicable here that most people engaged with this topic have not internalized?
5. THE EXCEPTION: Is there a historical case where the expected pattern did NOT hold — and what made it different?

Ground your analysis in specific historical events, eras, or cases. Avoid vague references to "history shows." Name the patterns and the periods.
```

After all 5 agents complete, collect their outputs and proceed to Phase 2.

---

## Phase 2 — Contradiction Map (SEQUENTIAL)

Using all 5 perspective outputs from Phase 1, produce a contradiction map. Do this yourself (no sub-agent needed — you have all the context).

Structure your contradiction map as follows:

**DIRECT CONTRADICTIONS**
List every place where two or more perspectives make claims that cannot both be true. For each conflict, name:
- The specific claims that clash
- Which perspectives hold each position
- What evidence each side has

**EVIDENCE RANKINGS**
For each major claim that appears across perspectives:
- Which perspective has the strongest evidentiary support?
- Which has the weakest? Why?

**THE RESOLUTION QUESTION**
What is the single question that, if answered with certainty, would resolve the biggest contradiction in the field?

**UNIVERSAL AGREEMENTS**
What does every perspective agree on — even the skeptic? (These are the most reliable facts about the topic.)

**THE BLIND SPOT**
What topic, angle, or question did NONE of the five perspectives address? This is often the most valuable finding — the gap in the entire field's thinking.

---

## Phase 3 — Synthesis (SEQUENTIAL)

Using Phase 1 outputs and the Phase 2 contradiction map, write a full research briefing. Do this yourself.

Structure:

**EXECUTIVE SUMMARY**
One paragraph (5–7 sentences) that explains the topic as if briefing a CEO who has 60 seconds. Must include: the core reality, the key tension or debate, and the most important nuance. No jargon. No hedging.

**5 KEY FINDINGS**
The five most important things now known about this topic, ranked by reliability. For each finding:
- The finding (1–2 sentences)
- Which perspectives support it
- Which perspectives challenge it
- Reliability rating: HIGH / MEDIUM / LOW with a one-sentence reason

**THE HIDDEN CONNECTION**
One non-obvious insight that only becomes visible when all five perspectives are considered together. This should be something that no single perspective could have surfaced alone.

**ACTIONABLE INSIGHT**
Based on all evidence, what should someone who cares about this topic actually DO differently right now? Be specific. If the topic is abstract (e.g., a scientific or historical subject), frame the action as: what to study next, what assumption to question, or what decision to make differently.

**THE FRONTIER QUESTION**
The one open question that, if answered, would most change how we understand this topic. Why is it unanswered? What would it take to answer it?

---

## Phase 4 — Peer Review (SEQUENTIAL)

Critically evaluate the research briefing from Phase 3. Do this yourself.

Structure:

**CONFIDENCE SCORES**
Rate each of the 5 key findings on a 1–10 scale for reliability.
- Score
- Reason for the score
- What specific information would be needed to raise the score to a 10

**WEAKEST LINK**
Which claim in the entire briefing are you least confident in? What would it take to verify or falsify it?

**BIAS AUDIT**
Which of the 5 perspectives had the most influence on the final synthesis? Is that influence justified by the strength of their evidence, or did one voice crowd out others?

**MISSING PERSPECTIVE**
Is there a 6th expert lens that was not included — one that, if added, would meaningfully change the conclusions? Describe it and what it would likely reveal.

**OVERALL GRADE**
If a Stanford professor reviewed this briefing, what letter grade would they give (A through F)? Give a one-paragraph justification: what is strong, what is weak, what would they tell you to fix before publication?

---

## Final Output — Compiled Research Paper

After completing all four phases, compile everything into a single, well-formatted research paper using this structure:

```
# STORM Research Paper: [Topic]
*Generated using the Stanford STORM Multi-Perspective Research Method*
*Date: [current date]*

---

## Executive Summary
[From Phase 3]

---

## Part I: Five Expert Perspectives

### 1. The Practitioner's View
[Phase 1, Agent 1 output — formatted cleanly]

### 2. The Academic's View
[Phase 1, Agent 2 output — formatted cleanly]

### 3. The Skeptic's View
[Phase 1, Agent 3 output — formatted cleanly]

### 4. The Economist's View
[Phase 1, Agent 4 output — formatted cleanly]

### 5. The Historian's View
[Phase 1, Agent 5 output — formatted cleanly]

---

## Part II: Where the Experts Disagree
[Phase 2 contradiction map]

---

## Part III: Synthesis and Key Findings
[Phase 3 briefing — executive summary already at top, so start with 5 Key Findings here]

---

## Part IV: Peer Review and Confidence Assessment
[Phase 4 full output]

---

## Appendix: Research Method
This paper was generated using the Stanford STORM method (Synthesis of Topic Outlines
through Retrieval and Multi-perspective Question Asking), adapted for use with Claude.
The method uses parallel expert-perspective agents to surface blind spots that single-
prompt research misses. Original research published at NAACL 2024 by the Stanford OVAL Lab.
```

After outputting the research paper, ask the user:
> "Would you like me to save this as a markdown file? If so, what filename would you like?"

If they say yes (or provide a filename), save the file to the current working directory as `[filename].md` using the Write tool.

---

## Important Notes for Execution

- **Do not wait** between phases. Execute Phase 1 agents in parallel, then proceed immediately through Phases 2–4.
- **Do not summarize** the perspective outputs when compiling — include the full content from each agent.
- **Do not ask** for confirmation at any phase boundary. Run the full pipeline start to finish.
- The paper should feel like it was written by a team of researchers, not a chatbot. Use clear headers, specific claims, and no filler language.
- If the topic is ambiguous, pick the most interesting and substantive interpretation and proceed.
