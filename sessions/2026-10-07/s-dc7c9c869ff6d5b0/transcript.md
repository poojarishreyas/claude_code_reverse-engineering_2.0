# /** * File-finding evaluation runner. * * For each task mined from a repository's bug-fix history: prepare a workspac...

| | |
| --- | --- |
| session | `s-dc7c9c869ff6d5b0` |
| model | `claude-opus-5-5` |
| started | 2026-10-07T10:42:01.382Z |
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
 * For each task mined from a repository's bug-fix history: prepare a workspace
 * with the fix's source reverted, confirm the fix's tests fail, run the agent
 * headless through the shipped base profile with the failing output as its
 * task, re-run the tests, and record file-finding metrics from the session.
 *
 * Usage:
 *   pnpm run eval:file-finding -- --repo <git repo> [--limit 10] [--out eval-results]
 *     [--install "pnpm install --prefer-offline"] [--keep] [--dry-run] [--hard] [--only <id,...>]
 *     [--agent dsh|claude-code] [--provider <id>] [--model <id>]
 *
 * `--dry-run` stops after preparing and validating each task, so it needs no
 * model key. A full run needs the provider key (DEEPSEEK_API_KEY by default).
 * `--hard` keeps only tasks where the failing test does not lead straight to
 * the fix (see `difficultyTags`), taken round-robin across those kinds.
 * `--agent claude-code` runs the installed `claude` CLI on the same tasks
 * instead, with the same prompt, scored by the same metrics. `--provider` and
 * `--model` pick the model for either agent; for Claude Code, `--provider`
 * names a provider in `--home-from` to use instead of its own login, so both
 * agents can run the same model.
 */

import { spawn } from 'node:child_process'
import { copyFile, mkdir, readFile, rm, writeFile } from 'node:fs/promises'
import { tmpdir } from 'node:os'
import { join, resolve } from 'node:path'
import { fileURLToPath } from 'node:url'
import { parseArgs } from 'node:util'
import { resolveExampleLaunch } from '@deepseek-ai/dsh-loader-smoke'
import { load } from 'js-yaml'
import { claudeCodeArgs, claudeCodeEnv, parseClaudeCodeOutput } from './claude-code.ts'
import type { ClaudeCodeProvider } from './claude-code.ts'
import { computeMetrics, promptTokens, summarize } from './metrics.ts'
import type { EvalEvent, EvalUsage, RunMetrics } from './metrics.ts'
import { difficultyTags, mineTasks, prepareWorkspace, readTestSources, removeWorkspace, taskPrompt } from './tasks.ts'
import type { EvalTask, TaskTag } from './tasks.ts'

const repoRoot = fileURLToPath(new URL('../../', import.meta.url))
const DRIVER = join(repoRoot, 'packages/test-support/loader-smoke/tests/fixtures/base-driver.ts')
const OVERLAY = join(repoRoot, 'scripts/eval/eval.cordis.yml')
const TSCONFIG = join(repoRoot, 'tsconfig.json')
const MAX_FAILURE_CHARS = 6_000
const LOCALE_FILE = /(^|\/)locales?(\/|\.ts$|\.tsx$)/

/** Outcome of one task. */
interface TaskResult {
  readonly task: EvalTask
  readonly tags: readonly TaskTag[]
  readonly status: 'valid' | 'invalid' | 'ran' | 'error'
  readonly passed: boolean
  readonly metrics?: RunMetrics
  readonly finalText?: string
  /** Model the endpoint reported answering, when the agent's output names it. */
  readonly model?: string
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
  // One worker: a task runs only a few spec files, and parallel workers can exhaust memory on a laptop.
  return exec('npx', ['vitest', 'run', '--maxWorkers=1', ...files], workspace, process.env, 15 * 6
... [16,063 more characters in session.jsonl]

#### ASSISTANT

_[empty]_

_stop `null` · 584ms · in 0 · out 0 · cache r0/w0_

