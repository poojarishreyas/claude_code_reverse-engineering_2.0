# Perform a web search for the query: Laya code retrieval graph tool coding agent

| | |
| --- | --- |
| session | `s-c6fecb85d6ff0cd7` |
| model | `claude-opus-5-5` |
| started | 2026-10-06T06:01:00.707Z |
| requests | 1 |
| tokens | in 12,173 · out 1,469 · cache read 0 · cache write 0 |

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

Perform a web search for the query: Laya code retrieval graph tool coding agent

#### ASSISTANT

```json
{
  "type": "server_tool_use",
  "id": "srvtoolu_01HQfQH2MM2XQEmMhuY8CczL",
  "name": "web_search",
  "input": {
    "query": "Laya code retrieval graph tool coding agent"
  }
}
```

```json
{
  "type": "web_search_tool_result",
  "tool_use_id": "srvtoolu_01HQfQH2MM2XQEmMhuY8CczL",
  "content": [
    {
      "type": "web_search_result",
      "title": "GitHub - Intelligent-Intern/layagrep: Local code retrieval for coding agents with Laya and optional CodeGraph · GitHub",
      "url": "https://github.com/Intelligent-Intern/layagrep",
      "encrypted_content": "EuAQCioIFBgCIiQ5OGE5NTJiZC0xYjViLTRhNTUtYjBjMC04ZWViNWFjMTFjZmYSDKtveTmRAUvJlkBfWhoMHduHE14r6QvaikC1IjBNG6DJ9nZU+ZBqXdoSlh4o1P8Uye/+T4a7F+JaQpsTFFpSfUIHkOl7og+jxtvRRPwq4w+8mrcAocX2P7LqBsOQA4wQtMC2vR/JATk8P9lY/P7yOClkMtzKfameHwKwuPhV6rEHiQDSokkge5RZVCQav3tfcybcMjfQ/BwTcgL/xYWbq1wtMGYeb5+gM9OtKFQXWC41KfU2GbOHO4pYGI8NKLFUTQ+qqqsnBvPgavVYZVVakODi6iA0saZrDlMBC0LxfcMrwy2DAi6HdpOxkJPpMFzHJCGyzcdU4Hni/iWjNs5tGjhDneaIvKlXeZ1Q4K4BJQ8AOrP/ElftQ+t3jrz2b2XXByqG6NdSw0mVKZANMDjm5ZUVk8I9CIaB6/cnatMswDLmDb3JlqQ+3f6P3eWM1ChCawZDk0xoVOsUlXPLOzEXJmDngO1caz25jhvqF8NIYMhjGVBDwT82SmVwcYBb+CA1lkCP0UbvIlfgbdMSHZnAOvYA42JMVMV9CoVfj5CLW1AOliuvfsAEzhx2r1tonBcBdjIsfyBWgMQle2rVDFIc4qdmER1fjoanyQ/8jS9Mm/J5fArKNlTV16ZqxxG3SUuL43ICfD3ztdWLKmGi2rAlaHPIuoTlwSklHWuxxsgVblNipJ1x/jUx0TcxZipwSrFE9FPfEVTF3a3qHBeOdPbxh6uGHfO5x9k8kuQRvRDs6cL3Cg2wSy0HU+j9Z921BQmx3FnwlMD2VzxqlOJmCT6GrvzQz1TvSn54RHHVFege8pZhYVuyMDe46533PMi054vFQdj5Q6Eei6/Shs5HvF88FHjBPvR4Vf7RQObjNdgUIX0zyrY4sWENyphp3OgqXJO7/9WqQvB47QvIuYPRGczr3gUjkO2MgScloMGlZGrH33Gw5r1NN7Yv2hDmjST1jHt6tUIQPI+KNkxL+wDXYrR91w4smmhGb2gHXjhTVuYfnezcWE1T5gi83C3dVfBEC2ACiUK+Qo3gwZ6Uu6t8gexhe2L9OlBXnaJ7SFWa
... [18,325 more characters in session.jsonl]
```

<details><summary>thinking</summary>

```

```

</details>

The closest match is **Layagrep**, an open-source GitHub project (Intelligent-Intern/layagrep) that uses Laya for local code retrieval and can optionally use CodeGraph.

**Layagrep**
- **What it is:** 

a local code retrieval CLI for coding agents.

 

It forks jevgrep (MIT) and replaces its hosted relevance decisions with Laya running on your machine.

 

You ask what the code does, and Layagrep returns relevant files, source excerpts, and line references.


- **Requirements:** 

Node.js 22+, Bun to build the checkout, Python 3.10+, and enough memory for a Laya checkpoint.

 

A CUDA GPU is optional.


- **Setup:** Install the server with `uv tool install 'laya[serve]'`, then start it with `laya-serve`. In another terminal, build and install the CLI and run queries such as 

`layagrep "Where is authentication checked before a request reaches a handler?"`


- **Endpoint and security:** 

The default endpoint is http://127.0.0.1:8000/v1.

 

If port 8000 is taken, you can set LAYAGREP_LAYA_URL to another port. Only loopback HTTP endpoints are accepted.

 

No external API key is needed.


- **Agent integration:** 

`layagrep skill` installs the bundled agent skill.

 

`jg` still works as an alias for existing scripts.


- **Caveats:** 

It uses Laya's multilingual checkpoint with a 4096-token request budget.

 The README says 

the fork hasn't reproduced jevgrep's published cost or retrieval benchmarks, so those upstream numbers don't establish Layagrep's quality.

 The README also describes a small agent benchmark, but it's cut off in the search results: one run on each of ten SWE-bench tasks, comparing results with and without the tool.

**Related research on graph-based code retrieval for agents**
- **RANGER:** This tool 

builds a knowledge graph of the whole repository, capturing hierarchical and cross-file dependencies down to the variable level.

 

Entity-based queries are answered with fast Cypher lookups, and natural-language queries use MCTS-guided graph exploration.


- **GraphCodeAgent:** 

It builds two linked graphs: a Requirement Graph and a Structural-Semantic Code Graph that captures the repository's code dependencies.


- **LARGER (Lexically Anchored Repository Graph Exploration and Retrieval):** The paper points out that CLI coding agents like Claude Code, Codex, and OpenCode rely on shell tools, and that 

this lexical-only interface leaves structural dependencies invisible unless surfaced through additional reasoning steps.


- **Coding-agent taxonomy:** A study of 13 agents found that 

eight of them (including SWE-agent, OpenHands, Codex CLI, and Gemini CLI) treat the LLM as a navigator using general shell tools like grep, find, and ripgrep.

 

The others build structured representations of the codebase before or during the task.

_stop `end_turn` · 13.79s (ttft 1.84s) · in 12,173 · out 1,469 · cache r0/w0_

