# Web page content: --- A deep dive into Jev, TypeSafe's System One model [Solo Lab: make a living from your own softwa...

| | |
| --- | --- |
| session | `s-49f66186d0bfb82f` |
| model | `claude-opus-5-5` |
| started | 2026-10-06T06:01:23.567Z |
| requests | 1 |
| tokens | in 27,261 · out 1,241 · cache read 0 · cache write 0 |

> Generated from `session.jsonl`. Delete this file and it regenerates.

---

### Context established — 0 tools

- system prompt: [`add65b88e16c1a39bb62e00f`](../../../objects/ad/add65b88e16c1a39bb62e00f.json)
- tool catalogue: [`4f53cda18c2baa0c0354bb5f`](../../../objects/4f/4f53cda18c2baa0c0354bb5f.json)

---

## req-0001 — claude-opus-5-5

_max_tokens 128,000 · streaming · 1 messages_

#### USER


Web page content:
---
A deep dive into Jev, TypeSafe's System One model    

[Solo Lab: make a living from your own software →](/courses/solo-lab/)A three-week intensive starting 28 October. The waiting list is open.

Sponsors [Creem](https://www.creem.io/?utm_source=flaviocopes.com&utm_medium=sponsor "Sell Software Globally - with zero headaches")[\+ Become a sponsor](/sponsor/)

[Sponsored CreemSell Software Globally - with zero headaches](https://www.creem.io/?utm_source=flaviocopes.com&utm_medium=sponsor)[+Become a sponsorGet your product in front of developers.](/sponsor/)

[← All posts](/blog/)

Blog post

A deep dive into Jev, TypeSafe's System One model

In this post

[What Jev is in one sentence](#what-jev-is-in-one-sentence)[How Jev differs from ChatGPT, Cursor, Codex and Claude Code](#how-jev-differs-from-chatgpt-cursor-codex-and-claude-code)[How Jev differs from classifiers and structured LLM outputs](#how-jev-differs-from-classifiers-and-structured-llm-outputs)[Where the name comes from](#where-the-name-comes-from)[How Jev works under the hood](#how-jev-works-under-the-hood)[The three question types](#the-three-question-types)[Noul: a yes/no question](#noul-a-yesno-question)[Choice: pick one option](#choice-pick-one-option)[Score: a position on a scale you describe](#score-a-position-on-a-scale-you-describe)[State: what you give Jev to look at](#state-what-you-give-jev-to-look-at)[Confidence: when to act and when to ask](#confidence-when-to-act-and-when-to-ask)[Is Jev open source? Can you run it locally?](#is-jev-open-source-can-you-run-it-locally)[Getting access](#getting-access)[Your first call with curl](#your-first-call-with-curl)[Using Jev from Node.js](#using-jev-from-nodejs)[Python in a few lines](#python-in-a-few-lines)[Using Jev through the Vercel AI SDK](#using-jev-through-the-vercel-ai-sdk)[Ask everything at once](#ask-everything-at-once)[Compose decisions in code](#compose-decisions-in-code)[Writing questions Jev answers well](#writing-questions-jev-answers-well)[Where Jev breaks](#where-jev-breaks)[What people are building with it](#what-people-are-building-with-it)[Labeling data](#labeling-data)[Routing and verification](#routing-and-verification)[Search](#search)[Inside apps that already exist](#inside-apps-that-already-exist)[Real-time interfaces](#real-time-interfaces)[Agents and tools](#agents-and-tools)[Feature engineering](#feature-engineering)[The skeptical notes](#the-skeptical-notes)[Jev and coding agents](#jev-and-coding-agents)[How I will use Jev in my workflows](#how-i-will-use-jev-in-my-workflows)[Route work before starting a coding agent](#route-work-before-starting-a-coding-agent)[Put a safety check in front of shell commands](#put-a-safety-check-in-front-of-shell-commands)[Prefilter the blog maintenance work](#prefilter-the-blog-maintenance-work)[Sort sponsor inquiries and newsletter replies](#sort-sponsor-inquiries-and-newsletter-replies)[Add semantic priority to Events Logger](#add-semantic-priority-to-events-logger)[Try it in the Bootcamp projects](#try-it-in-the-bootcamp-projects)[How I will roll this out](#how-i-will-roll-this-out)[What it costs, and how fast it is](#what-it-costs-and-how-fast-it-is)[Could Jev cut an AI bill by 50 or 60 percent?](#could-jev-cut-an-ai-bill-by-50-or-60-percent)[Where to start](#where-to-start)

[Home](/) / [AI](/tags/ai/)

A deep dive into Jev, TypeSafe's System One model
=================================================

By [Flavio Copes](/about/)

Updated Oct 1, 2026

Learn how Jev turns text into typed choices, scores, and probabilities, with JavaScript examples, practical patterns, limits, and real use cases.

\~~~

Jev is not a chatbot like ChatGPT, and it is not a coding model. It does not write replies, explanations, or code.

You send it data and a list of typed questions. It sends back one answer per question: a yes/no probability, one option from a list you defined, or a position on a scale you defined, each with probabilities. TypeSafe 
... [74,842 more characters in session.jsonl]

#### ASSISTANT

<details><summary>thinking</summary>

```

```

</details>

## Jev at a glance

**What it is:** Jev is a decision model from TypeSafe AI, which the company calls a "System One model." It doesn't write prose or code. You send it a state (text or JSON) and a set of typed questions, and it returns probabilities. The author describes it as a smart `if` statement.

**Model size:** Not disclosed. TypeSafe hasn't published a paper or its architecture. The launch post calls Jev "neither small nor an LLM" and skips public benchmarks.

**Latency:** TypeSafe quotes 70–500 ms end to end, with most calls around 100 ms. That's measured from the US West Coast, so expect extra network delay elsewhere.

**Pricing:**
- Input costs $0.042 per million tokens, and output is free.
- The same rate applies through Vercel's AI Gateway (`typesafe-ai/jev`).
- A ~300-token support ticket costs about $0.0000126.

**Hosted or local:**
- Jev is hosted only. Its weights aren't released and there's no self-hosted version.
- The SDKs (JavaScript and Python) and the agent skill are MIT-licensed.
- The closest local option is Cloudflare's **Clef**. It has Apache 2.0 open weights, is built on Qwen, and accepts Jev's request format. Cloudflare tested it on a single H200.
- Hugging Face "Open-Jev" models are community projects, not Jev itself.

**Tasks:** There are three question types:
- **Noul:** a yes/no probability.
- **Choice:** one option from up to 255, with probabilities and confidence.
- **Score:** a position on a 2–10 level scale.

Typical uses include labeling, routing, verification, re-ranking search results, and safety checks. It handles text only. It's weak at math, counting, dates, and writing.

**Context limits:**
- State plus all questions: about 64K tokens.
- State plus the longest single question: about 32K tokens, roughly 150K characters.

**Code retrieval:** The article doesn't mention "jevgrep." The closest project is **Oko**:
- It finds candidate snippets locally, has Jev rank them, and serves them to Codex, Claude Code, or OpenCode over MCP.
- On a public benchmark of 345 code-retrieval tasks in six languages, it scored MRR 0.39 versus 0.24 for other published methods.
- In its authors' own benchmark, agents finished tasks 12–38% faster.
- A `--no-jev` flag keeps everything local.

A related project, **jevsearch** (site search), reports a 278 ms median and $0.26 per 1,000 uncached searches. These are the builders' own numbers, not independent measurements.

_stop `end_turn` · 12.40s (ttft 4.75s) · in 27,261 · out 1,241 · cache r0/w0_

