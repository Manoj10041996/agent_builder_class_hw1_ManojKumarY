# Agent Builder — Homework 1: Agents Workbook

## What I built
Completed the Agents workbook by extending the NL-to-SQL pipeline into a multi-tool ReAct agent with 4 tools: `query_launches`, `vehicle_specs`, `compare`, and `random_number`.

## Tasks Completed

### Task 1 — Added `compare` tool
Added a third tool that compares two values side by side. The agent used it for height comparisons but skipped it when it could answer directly.

### Task 2 — Added `random_number` tool
Added a useless tool. The agent never called it for normal questions — only when explicitly asked for a random number.

### Task 3 — Added `crew_capacity` to `vehicle_specs.json`
Added a new key to the JSON file. The agent pulled it out correctly when asked how many crew Falcon 9 can carry.

### Task 4 — Temperature 0 vs 0.7
At temperature 0 every run gave identical wording. At 0.7 the facts stayed the same but phrasing changed each time.

### Task 5 — Weaker model behavior
Switched to a smaller model. It called the right tools but hallucinated wrong values inside `compare`. The final answer still sounded correct — dangerous without checking the trace.

### Task 6 — Messages grow with each step
Added `print(messages)` after the loop. Each step adds messages — the LLM receives the full conversation history every time.

## My Insights
My Insights — Agent Builder Workbook 2
1. Pipeline vs Agent
A pipeline blindly follows fixed steps every time. An agent thinks before acting — it looks at the question, picks the right tool, and decides when it has enough to answer. That flexibility is what makes agents actually useful.
2. The compare Tool
I expected the agent to use compare every time I asked a comparison question. It didn't. For height comparisons it called compare, but for launch counts it skipped it and answered directly. The agent decides — not me. Giving it a tool doesn't mean it will always use it.
3. Temperature 0 vs 0.7
At temperature 0 every run gave identical wording. At 0.7 the facts stayed the same but the phrasing changed each time. For production use, temperature 0 is safer. For conversational feel, 0.7 works better.
4. Weaker Model Behavior
The smaller model called the right tools and got correct data back — but then hallucinated wrong values when calling compare. The final answer still sounded correct. This was alarming. Without checking the full trace I would never have caught it.
5. How Messages Grow
Seeing the messages list grow in real time made memory finally click for me. The LLM remembers nothing — you hand it the entire conversation history every single step. For long runs this grows fast, which is exactly why max_iters matters.
6. Most Surprising Thing
The random_number tool was never called accidentally. The agent completely ignored it for every normal question. It only used it when I explicitly asked for a random number. A clear docstring is everything — it keeps the agent disciplined.
## Setup
```bash
cp .env.example .env
# Add your GROQ_API_KEY to .env
uv run jupyter lab agent.ipynb
```

## .env.example
```
GROQ_API_KEY=your_key_here
```