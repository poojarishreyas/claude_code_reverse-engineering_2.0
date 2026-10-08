# /** * pi-ai assistant event translation into the Harness streaming protocol. * * pi-ai tool-call arguments are parsed...

| | |
| --- | --- |
| session | `s-029ad50047a1f638` |
| model | `claude-opus-5-5` |
| started | 2026-10-08T08:39:53.625Z |
| requests | 1 |
| tokens | in 0 · out 0 · cache read 0 · cache write 0 |

> Generated from `session.jsonl`. Delete this file and it regenerates.

---

### Context established — 0 tools

- tool catalogue: [`4f53cda18c2baa0c0354bb5f`](../../../objects/4f/4f53cda18c2baa0c0354bb5f.json)

---

## req-0001 — claude-opus-5-5

_buffered · 1 messages_

#### USER

/**
 * pi-ai assistant event translation into the Harness streaming protocol.
 *
 * pi-ai tool-call arguments are parsed objects while the Harness keeps their
 * raw JSON representation. pi-ai also reports failures as terminal stream
 * events, which this module maps into Harness finish chunks.
 *
 * @module dsh-llm-pi-ai/stream
 */

import { brandString } from '@deepseek-ai/dsh-brand'
import { CONTEXT_WINDOW_EXCEEDED_CODE, EMPTY_RESPONSE_CODE, isContextWindowExceededError, isQuotaExceededError, LlmError, QUOTA_EXCEEDED_CODE } from '@deepseek-ai/dsh-llm'
import type { FinishReason, StreamChunk, TokenUsage, ToolCallId } from '@deepseek-ai/dsh-llm'
import { isContextOverflow } from '@earendil-works/pi-ai'
import type { AssistantMessage, AssistantMessageEvent, Usage as PiUsage } from '@earendil-works/pi-ai'
import { toPiReplayState } from './replay.ts'

/**
 * Map pi-ai usage (reasoning folded into output by pi-ai).
 * @param usage - cumulative usage from the terminal pi-ai event.
 * @returns harness counts with pi-ai's exact total; cache fields appear only
 *   when non-zero (pi-ai reports zeros, not absence).
 */
export function mapUsage(usage: PiUsage): TokenUsage {
  return {
    inputTokens: usage.input,
    outputTokens: usage.output,
    totalTokens: usage.totalTokens,
    ...usage.cacheRead > 0 ? { cacheReadTokens: usage.cacheRead } : {},
    ...usage.cacheWrite > 0 ? { cacheWriteTokens: usage.cacheWrite } : {},
  }
}

// XXX(pi-ai upstream): pi-ai flattens the caught error to `error.message`
// (api/anthropic-messages.js: `errorMessage = error instanceof Error ?
// error.message : JSON.stringify(error)`), discarding the original Error and its
// `cause` chain before it reaches us. undici carries the actionable transport
// detail on `cause` (e.g. `SocketError: other side closed`) but hands the fetch
// wrapper a bare `terminated`, so we are left pattern-matching terse words here.
// If pi-ai ever forwards the original Error (or a fetch/dispatcher hook that lets
// us capture the cause ourselves), classify on `code`/`cause` instead of text.
// The first standalone 4xx/5xx number is the status. Digits inside addresses
// and ports are not: OmniRoute reports a `[502]: fetch failed` whose cause lists
// IPv6 addresses such as `2001:4860:4844:400::`, and that 400 is not the status.
function httpStatus(message: string): number | undefined {
  const match = /(?<![\w.:/-])[45]\d\d(?![\w.])/.exec(message)
  return match === null ? undefined : Number(match[0])
}

function classifyPiAiError(message: string): string {
  const status = httpStatus(message)
  if (status === 401 || status === 403) return 'AUTH'
  if (isQuotaExceededError(message)) return QUOTA_EXCEEDED_CODE
  // Gateways such as OmniRoute report a brief credential cooldown without a
  // status code: `All credentials for model … are cooling down (reset after 5s)`.
  if (status === 429 || /rate.?limit|cooling down/i.test(message)) return 'RATE_LIMIT'
  // A rejected request body (gateway or provider size cap): resending the
  // same request cannot succeed, so it is invalid, not transient.
  if (status === 413 || /failed to buffer the request body:\s*length limit exceeded|payload too large|request body too large/i.test(message)) return 'INVALID_REQUEST'
  if (status === 400 || /invalid.?request/i.test(message)) return 'INVALID_REQUEST'
  if (status !== undefined && status >= 500) return 'SERVER'
  if (/\btime(?:d)?\s*out\b|timeout/i.test(message)) return 'TIMEOUT'
  // A stream truncated before the provider's terminal event: each pi-ai provider
  // throws its own wording when the wire closes mid-response without a terminal
  // event (`… stream ended before message_stop`, `… before a terminal response
  // event`, `… ended without a terminal event`, `Stream ended without
  // finish_reason`). The connection dropped mid-response, so this is a transport
  // truncation, not a model-level error.
  if (/stream ended (?:before|without)\b/i.test(message)) return 'TRANSPORT'
 
... [7,296 more characters in session.jsonl]

#### ASSISTANT

_[empty]_

_stop `null` · 678ms · in 0 · out 0 · cache r0/w0_

