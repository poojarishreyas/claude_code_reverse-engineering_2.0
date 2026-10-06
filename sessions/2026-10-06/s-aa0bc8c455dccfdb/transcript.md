# Perform a web search for the query: jev code graph tool coding agent

| | |
| --- | --- |
| session | `s-aa0bc8c455dccfdb` |
| model | `claude-opus-5-5` |
| started | 2026-10-06T06:01:00.727Z |
| requests | 1 |
| tokens | in 12,967 · out 1,435 · cache read 0 · cache write 0 |

> Generated from `session.jsonl`. Delete this file and it regenerates.

---

### Context established — 1 tools

- system prompt: [`cdd45a630f25f61bc4927562`](../../../objects/cd/cdd45a630f25f61bc4927562.json)
- tool catalogue: [`d7a64925cd9e1330abf18ea8`](../../../objects/d7/d7a64925cd9e1330abf18ea8.json)
- tools: `web_search`

---

## req-0001 — claude-opus-5-5

_max_tokens 128,000 · streaming · 1 messages_

#### USER

Perform a web search for the query: jev code graph tool coding agent

#### ASSISTANT

```json
{
  "type": "server_tool_use",
  "id": "srvtoolu_01KiaBjiGeWh1C2gak4SpoE2",
  "name": "web_search",
  "input": {
    "query": "jev code graph tool coding agent"
  }
}
```

```json
{
  "type": "web_search_tool_result",
  "tool_use_id": "srvtoolu_01KiaBjiGeWh1C2gak4SpoE2",
  "content": [
    {
      "type": "web_search_result",
      "title": "GitHub - merijjeyn/jive: A terminal coding agent that plans work as executable graphs · GitHub",
      "url": "https://github.com/merijjeyn/jive",
      "encrypted_content": "EuAQCioIFBgCIiQ5OGE5NTJiZC0xYjViLTRhNTUtYjBjMC04ZWViNWFjMTFjZmYSDGXAvu/kWT+ruVoRYhoMndALjDdvD8xJxUTlIjAAwGQ73sKFOo8kNIJN1y2NUgqb3fB9ihIzym3nY9ugvY5ieOsHjqwzSLJ1i56tg9Mq4w8jTSbuLrO4GB942/VNd+axY4ldpNq1ZsPy+teA9xk60PhcYkxN2pYOZKGTk50E6EgzweJRBuRZWSFKeW1Rb/29LCNw3iprgeUrwFT8n+lWM2MgvJti/IFAt0kxc16MpeqZu/3iRwLGf2j5Y+26xlbZk/JmVbR5WzreojHwOHG87+Zm/E3JoqJNBRTnip4hBhRY43SP3wfww+mOxlKLTkAPh2HfLODlPodoOjuxzCjouBVAkRxIj2Vqj/W4XT7ksWTYE2EaNcHIB1dElfg9mHR5jDIrGRkbDu74xQV8oTK1wTBDDGEpZujtvlJxL0OycpuFashMzD8YdIQCtVY8wsam3sIZ1Vm/fw0uthUEHfEWNK4mmJFe6RhXjzlNFpc1tnNWHZHdroWEDIGeThp65ti/LxlCVT1JUrAaVG8iI7hUg/WcQyFNxitnBfJmiREPzuMIE3I0UM8kijstJg+od8i2fSOW1kVMeS3JFJsSb5HIkO2iHO0dzYiPQa8hs3Jt2w9uUMCpuxcM1hLbUh3pqAM3ipJAKll50n/kgyl4TVyHQ5kNjmHxb6Q6qZ53FvglsrPmBbLK0MZ19U+PYdlIsba8o7vb1E/XO7ixC91FF5QxVhrNJSWmDkZFINKKCjONDuDpsz4T3U2lzwtyUS5uBMicKnjRANS0rWNgYsvxHgDBJYnB+WTyglzfjf0ynaa1d3c2zgIuaDWqKxXQdyL5LMvYUOZkUihsLwKohYZy88stJFQEMUNz1a2m3kVRlm5VFo793ILMhtR/eEpT0f0pfUyECkTR0onHrTbGkRfGxs2uFQhcjcwLKKw3GSzO7b7OfGIHr9SawjNWWeUzclioM9VVvkOIbbWTysnZk34XvMwCS0RRwRXCBgqUZfEzZXAIV9VebxV3RPDOohpEL8iunSg4PJutQjDAsXemgmQDUE0BhzBL7cSWEgEWyCEd5+DfyBkK9clqRmNXJrssC0Wqh+23y819IHa3X
... [20,223 more characters in session.jsonl]
```

<details><summary>thinking</summary>

```

```

</details>

Jev is a "System One" decision model from TypeSafe AI, not a coding model. The search turned up a few new open-source projects that plug it into coding agents. The closest match to "code graph" is **Jive**.

## Jive: a coding agent that plans work as graphs
- **What it is:** Jive is 

a terminal coding agent that plans work as executable graphs

 (GitHub: merijjeyn/jive, about 10 days old).
- **How it works:** 

Jive replaces "Tool Calls" with "Graph Calls", where each graph is a DAG-based workflow compromising of Tool Calls and Jev Calls.

 The goal is for the agent to 

do its hard reasoning using the power of modern LLMs, capture an execution graph filled with steps and fast intuitive decisions, and prevent it from making LLM calls for just to "follow through the plan".


- **Claimed results:** The author's own benchmark says that on the conversation_eval task, Jive finished in 

3m 26s

, compared with 29m 33s for Codex and 16m 48s for Claude Code. It also used far fewer LLM calls and output tokens. No one else has tested these numbers.

## Other projects that use Jev with coding agents
- **jev-code** (FrancoisChastel/jev-code): makes Jev 

a tool inside Claude Code, Codex, Pi, and OpenCode.

 It provides five tools: 

jev\_classify, jev\_check, jev\_score, jev\_rank, jev\_ask.

 One setup command 

detects Claude Code, Codex, Pi, and OpenCode on your machine and wires both the skill and the tool into each.


- **jev-gateway** (vinilana/jev-gateway): a local gateway. 

When your agent is about to decide which tool to call, the gateway asks Jev, TypeSafe's fast decision model, instead of leaving that choice to the expensive reasoning model.

 It 

works with Codex, Claude Code, OpenCode and Kilo out of the box

. It is an 

independent project, not affiliated with or endorsed by TypeSafe.



## What Jev is
- TypeSafe's documentation says 

Jev is not a drop-in replacement for the LLM behind Claude Code, Cursor, opencode, Copilot

, and similar tools. 

It does not generate text, write code, or hold a conversation.


- Instead, Jev 

gives it one state and a set of questions. It returns typed answers and probabilities, then stops.


- One example from Firecrawl's write-up uses Jev to 

judge coding-agent tool calls before they run

, for instance to flag commands that can't be undone or that have nothing to do with the task.

## Related research (no Jev involved)
If you meant code graphs in general:
- **LocAgent** gives agents a graph tool that allows 

arbitrary multihop codebase navigation through only one action

.
- **GraphCodeAgent** uses dual graphs to guide code generation across a whole repository.

_stop `end_turn` · 14.37s (ttft 2.15s) · in 12,967 · out 1,435 · cache r0/w0_

