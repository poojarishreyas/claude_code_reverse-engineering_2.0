# /** * File-finding evaluation runner. * * For each task mined from a repository's bug-fix history: prepare a worktree...

| | |
| --- | --- |
| session | `s-b4438aa44346e089` |
| model | `claude-opus-5-5` |
| started | 2026-10-05T11:16:10.983Z |
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
 * File-finding evaluation runner.
 *
 * For each task mined from a repository's bug-fix history: prepare a worktree
 * with the fix's source reverted, confirm the fix's tests fail, run the agent
 * headless through the shipped base profile with the failing output as its
 * task, re-run the tests, and record file-finding metrics from the session.
 *
 * Usage:
 *   pnpm run eval:file-finding -- --repo <git repo> [--limit 10] [--out eval-results]
 *     [--install "pnpm install --prefer-offline"] [--keep] [--dry-run]
 *
 * `--dry-run` stops after preparing and validating each task, so it needs no
 * model key. A full run needs the provider key (DEEPSEEK_API_KEY by default).
 */

import { spawn } from 'node:child_process'
import { copyFile, mkdir, rm, writeFile } from 'node:fs/promises'
import { tmpdir } from 'node:os'
import { join, resolve } from 'node:path'
import { fileURLToPath } from 'node:url'
import { parseArgs } from 'node:util'
import { resolveExampleLaunch } from '@deepseek-ai/dsh-loader-smoke'
import { computeMetrics, summarize } from './metrics.ts'
import type { EvalEvent, EvalUsage, RunMetrics } from './metrics.ts'
import { mineTasks, prepareWorkspace, removeWorkspace, taskPrompt } from './tasks.ts'
import type { EvalTask } from './tasks.ts'

const repoRoot = fileURLToPath(new URL('../../', import.meta.url))
const DRIVER = join(repoRoot, 'packages/test-support/loader-smoke/tests/fixtures/base-driver.ts')
const OVERLAY = join(repoRoot, 'scripts/eval/eval.cordis.yml')
const TSCONFIG = join(repoRoot, 'tsconfig.json')
const MAX_FAILURE_CHARS = 6_000
const LOCALE_FILE = /(^|\/)locales?(\/|\.ts$|\.tsx$)/

/** Outcome of one task. */
interface TaskResult {
  readonly task: EvalTask
  readonly status: 'valid' | 'invalid' | 'ran' | 'error'
  readonly passed: boolean
  readonly metrics?: RunMetrics
  readonly finalText?: string
  readonly note?: string
}

interface Command {
  readonly code: number | null
  readonly stdout: string
  readonly stderr: string
}

function exec(command: string, args: readonly string[], cwd: string, env: NodeJS.ProcessEnv, timeoutMs: number): Promise<Command> {
  return new Promise((resolvePromise) => {
    const child = spawn(command, args, { cwd, env, shell: process.platform === 'win32' && !command.endsWith('.exe'), stdio: ['ignore', 'pipe', 'pipe'] })
    let stdout = ''
    let stderr = ''
    child.stdout.setEncoding('utf8').on('data', (chunk: string) => { stdout += chunk })
    child.stderr.setEncoding('utf8').on('data', (chunk: string) => { stderr += chunk })
    const timer = setTimeout(() => { child.kill('SIGKILL') }, timeoutMs)
    child.on('close', (code) => {
      clearTimeout(timer)
      resolvePromise({ code, stdout, stderr })
    })
  })
}

function runTests(workspace: string, files: readonly string[]): Promise<Command> {
  return exec('npx', ['vitest', 'run', ...files], workspace, process.env, 15 * 60_000)
}

function tail(text: string, max: number): string {
  return text.length <= max ? text : `[... ${text.length - max} earlier characters omitted ...]\n${text.slice(-max)}`
}

/** Parse the driver's JSONL stdout into session events and the final result row. */
function parseDriverOutput(stdout: string): { events: EvalEvent[]; usage?: EvalUsage; output?: string } {
  const events: EvalEvent[] = []
  let usage: EvalUsage | undefined
  let output: string | undefined
  for (const line of stdout.split('\n')) {
    if (!line.startsWith('{')) continue
    let row: { type?: string; event?: EvalEvent; usage?: EvalUsage; output?: string }
    try {
      row = JSON.parse(line) as typeof row
    } catch {
      // Non-JSON log lines from plugins are not events.
      continue
    }
    if (row.type === 'session_event' && row.event !== undefined) events.push(row.event)
    if (row.type === 'result') {
      usage = row.usage
      output = row.output
    }
  }
  return { events, ...usage === undefined ? {} : { usage }, ...output === undefined ? {} : { output } }
}

/** The error message 
... [7,570 more characters in session.jsonl]

#### ASSISTANT

_[empty]_

_stop `null` · 524ms · in 0 · out 0 · cache r0/w0_

