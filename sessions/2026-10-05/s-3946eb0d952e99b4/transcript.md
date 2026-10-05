# Perform a web search for the query: AIRCoder Adaptive Integration of Multi-dimensional Retrieval Repository-level Cod...

| | |
| --- | --- |
| session | `s-3946eb0d952e99b4` |
| model | `claude-opus-5-5` |
| started | 2026-10-05T20:11:29.656Z |
| requests | 1 |
| tokens | in 12,626 · out 922 · cache read 0 · cache write 0 |

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

Perform a web search for the query: AIRCoder Adaptive Integration of Multi-dimensional Retrieval Repository-level Code Completion ACL 2026

#### ASSISTANT

```json
{
  "type": "server_tool_use",
  "id": "srvtoolu_01FFKy7y3pnEE4Mg6cpzDPwA",
  "name": "web_search",
  "input": {
    "query": "AIRCoder Adaptive Integration Multi-dimensional Retrieval Repository-level Code Completion"
  }
}
```

```json
{
  "type": "web_search_tool_result",
  "tool_use_id": "srvtoolu_01FFKy7y3pnEE4Mg6cpzDPwA",
  "content": [
    {
      "type": "web_search_result",
      "title": "AIRCoder: Adaptive Integration of Multi-dimensional Retrieval for Repository-level Code Completion - ACL Anthology",
      "url": "https://aclanthology.org/2026.acl-long.1166/",
      "encrypted_content": "EuAQCioIFBgCIiQ5OGE5NTJiZC0xYjViLTRhNTUtYjBjMC04ZWViNWFjMTFjZmYSDKlDUnnZ36y/jdQs8hoMiFfzBNJKN4Lp+MqNIjCIxKMeuQlltqxIAeA2GIi93Z1bxL819aXTbBuX8Fqz44ApB3voHG6rFlsGWkoFgDEq4w+qocHfuGW/W0gNaJY9qEyahXsjAc9Q+n259i6LF1h5GUoR3FQC/HwhDBBGD3TfFIBQ9gTVGwxJ3BcnBxCt9iAMKoDOXZvEPClEHNjYSE1a4/mfS4yNuWbVFInBQPITRgOyVcEFRnXLO5Yi22qJb2/lMwtZou9Ch9DZuWZCfx7qm/HN0FfF39JB3TN5CoM5zhy19KAzxdwZB/UY0F2pti9KVXiPL1/SG151MIfoTyXTIGS63yjGBHP4MTBd9IX2tqWQoN8+oxxOIBt3XQtwcpoULMxpx5joI/UlpI85uj4M/5UHrDkfvzrt8mDnZNjv1K6N3kL2lwWJtMQs8ipqdK0D2g6TmotrM8qZTFTLMyN8reakfQsMzypPZN6NYlf9cI3h/EZVX3H+qMOBAhy9qT6266o0ClmcOeczOB84wKGxXO7zSNSRH5ouDMcJocgyNjjnWxjDcSesqUv/ahHBvQPZoL/iwalMidQjGqA1zgheEL+1WFBslsko/a3Oh7YO1y5rc/W8aW6iBuB2NQsa+VQbJ3BEzuZc5XAvem3l4cK7k69QxFW2CKfiH6kvrrK3tVjBsnvlQm/BtrU5ZtWDD0DL8FbYZJoVJniAOGuFShKAn/qkqsIZy571WXh2qSxk/MyKQbgOqbyxReMsEuSaryGSjPVM78O14O4SYC40cfDeWPT0kfa+lXmv1a8rFIdM7S0yoszbhF8+3/v3TQrsVgBVVAq1WLod5Cry+6+PIz+78/nFj53fLwhKkUTmJQC1KN406y8bUZXCfV2xMbOVHhZlUdEjonSjzFZ/ab4Pi6yErJne7R9YGxr4S9UrXw/+/uMtJTAFm6VghrA5egY4pp8lV+YRaeqH56LBAUt05nte8kdCJnVptlJYEd9ae+pMHe8IrufW97kE7p21/+FlFer6itJbL0MysSgtnmON4kn4AR1H2KrialJoMKalM+quRx
... [18,274 more characters in session.jsonl]
```

<details><summary>thinking</summary>

```

```

</details>

I found the paper. It's in the ACL Anthology as part of the ACL 2026 main conference proceedings.

**Paper details**
- **Title:** AIRCoder: Adaptive Integration of Multi-dimensional Retrieval for Repository-level Code Completion
- **Authors:** 

Chuanqi Shi, Miao Gao, Zhiqiang Gao


- **Venue:** 

Proceedings of the 64th Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers), July 2026, San Diego, California, United States


- **Anthology ID / pages:** 2026.acl-long.1166, 

pages 25458–25470


- **Link:** https://aclanthology.org/2026.acl-long.1166/ (PDF: https://aclanthology.org/2026.acl-long.1166.pdf)
- **Informal citation:** 

Shi et al., ACL 2026

, BibTeX key `shi-etal-2026-aircoder`

**Method:** 

AIRCoder uses a structure-preserving chunking strategy and a lightweight fusion module. It learns context-dependent weights so it can adaptively combine retrieval metrics for each query.



**Results:** 

On CrossCodeEval and RepoEval, AIRCoder improves exact match by 4.63% on average over the best baseline. It is also 10.2× more efficient and generalizes well across Python, Java, C#, and TypeScript.



**Related work:** The search also turned up other repository-level code completion methods, which may be useful for comparison:
- RepoCoder, which uses iterative retrieval and generation
- DraCo, which 

uses dataflow analysis to retrieve dependency contexts such as function or class definitions


- ProCC, which 

uses prompt engineering and a contextual multi-armed bandit algorithm to combine and adapt to multiple views of the code


- SaraCoder, a 

hierarchical, resource-optimized retrieval-augmented code completion framework

_stop `end_turn` · 9.14s (ttft 1.90s) · in 12,626 · out 922 · cache r0/w0_

