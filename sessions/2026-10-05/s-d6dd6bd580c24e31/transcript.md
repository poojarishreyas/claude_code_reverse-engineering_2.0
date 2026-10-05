# /** * File-finding metrics computed from one agent run's session events. * * Pure: the runner streams canonical sessi...

| | |
| --- | --- |
| session | `s-d6dd6bd580c24e31` |
| model | `claude-opus-5-5` |
| started | 2026-10-05T11:16:11.003Z |
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
 * File-finding metrics computed from one agent run's session events.
 *
 * Pure: the runner streams canonical session events from the base driver and
 * passes them here with the task's expected source files.
 */

import { isAbsolute, relative, resolve } from 'node:path'

/** The subset of a canonical session event the metrics read. */
export interface EvalEvent {
  readonly type: string
  readonly data: Record<string, unknown>
}

/** Token totals reported by the driver's result line. */
export interface EvalUsage {
  readonly inputTokens: number
  readonly outputTokens: number
  readonly cacheReadTokens?: number
}

/** What the task's real fix touched. */
export interface EvalExpectation {
  /** Workspace root the agent ran in; tool paths are resolved against it. */
  readonly workspace: string
  /** Source files the real fix changed, workspace-relative with `/` separators. */
  readonly sourceFiles: readonly string[]
  /** Test files that define success; editing them does not count as a fix. */
  readonly testFiles: readonly string[]
}

/** File-finding and cost metrics for one run. */
export interface RunMetrics {
  readonly steps: number
  readonly toolCalls: Readonly<Record<string, number>>
  /** First step whose tool activity named an expected source file (search hit or read), or null. */
  readonly firstSeenStep: number | null
  /** First step that read an expected source file, or null. */
  readonly firstReadStep: number | null
  /** `read` calls made before the first read of an expected source file (all reads when never read). */
  readonly readsBeforeCorrect: number
  /** Workspace-relative files the agent wrote or edited, sorted. */
  readonly editedFiles: readonly string[]
  /** Whether at least one expected source file was edited. */
  readonly editedExpected: boolean
  /** Edited files that are neither expected sources nor the task's tests. */
  readonly extraEdits: readonly string[]
  /** Whether a task test file was edited, which the task forbids. */
  readonly editedTests: boolean
  readonly usage?: EvalUsage
}

const READ_TOOLS = new Set(['read'])
const EDIT_TOOLS = new Set(['edit', 'write', 'str_replace_editor'])

/**
 * Compute the metrics for one run.
 * @param events - the run's session events in log order.
 * @param expected - the task's workspace and real-fix files.
 * @param usage - token totals from the driver's result line, when reported.
 * @returns the run's metrics.
 */
export function computeMetrics(
  events: readonly EvalEvent[],
  expected: EvalExpectation,
  usage?: EvalUsage,
): RunMetrics {
  const sources = new Set(expected.sourceFiles)
  const tests = new Set(expected.testFiles)
  const toolCalls: Record<string, number> = {}
  const edited = new Set<string>()
  const found = { step: 0, steps: 0, seen: null as number | null, read: null as number | null, readsBefore: 0 }

  const noteSeen = (): void => { found.seen ??= found.step }
  const visitCall = (name: string, args: unknown): void => {
    toolCalls[name] = (toolCalls[name] ?? 0) + 1
    const path = workspacePath(expected.workspace, filePathOf(args))
    if (READ_TOOLS.has(name)) {
      if (path !== undefined && sources.has(path)) {
        found.read ??= found.step
        noteSeen()
      } else if (found.read === null) {
        found.readsBefore += 1
      }
    }
    if (EDIT_TOOLS.has(name) && path !== undefined) edited.add(path)
  }

  for (const event of events) {
    switch (event.type) {
      case 'step/start':
        found.step = typeof event.data.step === 'number' ? event.data.step : found.step + 1
        found.steps += 1
        break
      case 'tool/call':
        visitCall(String(event.data.name), parseArguments(event.data.arguments))
        break
      case 'tool/code-dispatch':
        visitCall(String(event.data.name), event.data.arguments)
        if (found.seen === null && mentionsAny(event.data.content, expected.sourceFiles)) noteSeen()
        break
      case 'tool/result':
        if (found.seen ===
... [3,475 more characters in session.jsonl]

#### ASSISTANT

_[empty]_

_stop `null` · 565ms · in 0 · out 0 · cache r0/w0_

