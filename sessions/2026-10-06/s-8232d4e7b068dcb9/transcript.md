# Web page content: --- GitHub - Intelligent-Intern/layagrep: Local code retrieval for coding agents with Laya and opti...

| | |
| --- | --- |
| session | `s-8232d4e7b068dcb9` |
| model | `claude-opus-5-5` |
| started | 2026-10-06T06:01:24.160Z |
| requests | 1 |
| tokens | in 7,626 · out 911 · cache read 0 · cache write 0 |

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
                                                                                                                   GitHub - Intelligent-Intern/layagrep: Local code retrieval for coding agents with Laya and optional CodeGraph · GitHub                                             

[Skip to content](#start-of-content)     

   

           

Navigation Menu
---------------

[](/)

[Sign in](/login?return_to=https%3A%2F%2Fgithub.com%2FIntelligent-Intern%2Flayagrep)

Appearance settings

*   Platform
    
    *   AI CODE CREATION
        
        *   [GitHub CopilotWrite better code with AI](https://github.com/features/copilot)
        *   [GitHub Copilot appDirect agents from issue to merge](https://github.com/features/ai/github-app)
        *   [MCP RegistryIntegrate external tools](https://github.com/mcp)
        
    *   DEVELOPER WORKFLOWS
        
        *   [ActionsAutomate any workflow](https://github.com/features/actions)
        *   [CodespacesInstant dev environments](https://github.com/features/codespaces)
        *   [IssuesPlan and track work](https://github.com/features/issues)
        *   [Code ReviewManage code changes](https://github.com/features/code-review)
        *   [Code QualityEnforce quality at merge](https://github.com/features/code-quality)
        
    *   APPLICATION SECURITY
        
        *   [GitHub Advanced SecurityFind and fix vulnerabilities](https://github.com/security/advanced-security)
        *   [Code securitySecure your code as you build](https://github.com/security/advanced-security/code-security)
        *   [Secret protectionStop leaks before they start](https://github.com/security/advanced-security/secret-protection)
        
    *   EXPLORE
        
        *   [Why GitHub](https://github.com/why-github)
        *   [Documentation](https://docs.github.com)
        *   [Blog](https://github.blog)
        *   [Changelog](https://github.blog/changelog)
        *   [Marketplace](https://github.com/marketplace)
        
    
    [View all features](https://github.com/features)
    
*   Solutions
    
    *   BY COMPANY SIZE
        
        *   [Enterprises](https://github.com/enterprise)
        *   [Small and medium teams](https://github.com/team)
        *   [Startups](https://github.com/enterprise/startups)
        *   [Nonprofits](https://github.com/solutions/industry/nonprofits)
        
    *   BY USE CASE
        
        *   [App Modernization](https://github.com/solutions/use-case/app-modernization)
        *   [DevSecOps](https://github.com/solutions/use-case/devsecops)
        *   [DevOps](https://github.com/solutions/use-case/devops)
        *   [CI/CD](https://github.com/solutions/use-case/ci-cd)
        *   [View all use cases](https://github.com/solutions/use-case)
        
    *   BY INDUSTRY
        
        *   [Healthcare](https://github.com/solutions/industry/healthcare)
        *   [Financial services](https://github.com/solutions/industry/financial-services)
        *   [Manufacturing](https://github.com/solutions/industry/manufacturing)
        *   [Government](https://github.com/solutions/industry/government)
        *   [View all industries](https://github.com/solutions/industry)
        
    
    [View all solutions](https://github.com/solutions)
    
*   Resources
    
    *   EXPLORE BY TOPIC
        
        *   [AI](https://github.com/resources/articles?topic=ai)
        *   [Software Development](https://github.com/resources/articles?topic=software-development)
        *   [DevOps](https://github.com/resources/articles?topic=devops)
        *   [Security](https://github.com/resources/articles?topic=security)
        *   [View all topics](https://github.com/resources/articles)
        
    *   EXPLORE BY TYPE
        
        *   [Customer stories](https://github.com/customer-stories)
        *   [Events & webinars](https://github.com/resources/events)
        *   [Ebooks & reports](https://github.com/resources/whitepapers)
        * 
... [14,688 more characters in session.jsonl]

#### ASSISTANT

<details><summary>thinking</summary>

```

```

</details>

**Laya**

- **What it does:** Laya is the local model that replaces jevgrep's hosted relevance step. It decides which code is relevant on your own machine.
- **Setup:** You install it with `uv tool install 'laya[serve]'` and run it as a server (`laya-serve`). The default endpoint is `http://127.0.0.1:8000/v1`.
- **Configuration:** Layagrep explicitly selects Laya's "multilingual checkpoint" with "a 4096-token request budget."
- **License:** Laya is Apache-2.0. It is installed separately and not bundled with Layagrep.
- **Memory:** The page only says you need "enough memory for a Laya checkpoint." A CUDA GPU is optional.
- **Model size:** Not stated on the page.

**jevgrep**

- It is the MIT-licensed upstream project (dzhng/jevgrep) that Layagrep forks.
- It made relevance decisions through a hosted service, which Layagrep swaps for local Laya.
- **Pipeline and indexing:** The page gives no details on how jevgrep works internally.
- **Benchmarks:** jevgrep has published cost and retrieval benchmarks, but the page gives no numbers. The fork says it "has not reproduced jevgrep's published cost or retrieval benchmarks." It adds that those upstream results "do not establish Layagrep's quality."

**Agent benchmark (GPT-6 Sol, 10 SWE-bench tasks, one run each, CodeGraph off)**

| | Without Layagrep | With Layagrep |
|---|---|---|
| Officially resolved | 7/10 | 7/10 |
| Total agent time | 20 min 19 s | 27 min 18 s |
| Est. API cost | $2.31 | $2.63 |

- "Layagrep produced no additional solves in this run."
- Runs with the skill took "about 34% longer" and used "about 14% more model API spend."
- `pylint-dev__pylint-4604` was inconclusive in both arms because the grader collected no tests.
- A skill setup failure was left out of the paired results. It cost "an additional estimated $0.12."
- Reported costs exclude local Laya compute.
- The authors say the results don't show how Layagrep performs on other repositories or configurations.

_stop `end_turn` · 8.63s (ttft 2.45s) · in 7,626 · out 911 · cache r0/w0_

