# import { execFile } from 'node:child_process' import { mkdir, mkdtemp, readFile, rm, writeFile } from 'node:fs/promis...

| | |
| --- | --- |
| session | `s-626cca78a07b54c7` |
| model | `claude-opus-5-5` |
| started | 2026-10-07T10:42:01.394Z |
| requests | 2 |
| tokens | in 0 · out 0 · cache read 0 · cache write 0 |

> Generated from `session.jsonl`. Delete this file and it regenerates.

---

### Context established — 0 tools

- tool catalogue: [`4f53cda18c2baa0c0354bb5f`](../../../objects/4f/4f53cda18c2baa0c0354bb5f.json)

---

## req-0001 — claude-opus-5-5

_buffered · 1 messages_

#### USER

import { execFile } from 'node:child_process'
import { mkdir, mkdtemp, readFile, rm, writeFile } from 'node:fs/promises'
import { tmpdir } from 'node:os'
import { join } from 'node:path'
import { promisify } from 'node:util'
import { afterEach, describe, expect, it } from 'vitest'
import { classifyCommit, difficultyTags, mineTasks, packageOf, parseGitLog, prepareWorkspace, removeWorkspace, taskPrompt } from './tasks.ts'

const git = promisify(execFile)
let root: string | undefined

afterEach(async () => {
  if (root !== undefined) await rm(root, { recursive: true, force: true })
  root = undefined
})

describe('classifyCommit', () => {
  const src = 'packages/core/session/src/index.ts'
  const spec = 'packages/core/session/tests/session.spec.ts'

  it('accepts a small fix with source and spec changes', () => {
    expect(classifyCommit('fix(session): keep order', [src, spec, 'README.md'])).toEqual({ sourceFiles: [src], testFiles: [spec] })
    expect(classifyCommit('Prevent a double append', [src, spec])).toBeDefined()
    expect(classifyCommit('Tidy things', [src, spec, '.agents/notes/implemented/bug-fix/2026-01-01-x.md'])).toBeDefined()
    expect(classifyCommit('fix(app): x', ['apps/server/src/main.ts', 'apps/server/tests/main.spec.ts'])).toBeDefined()
  })

  it('rejects non-fixes, missing tests, declaration-only, and oversized commits', () => {
    expect(classifyCommit('Add a feature', [src, spec])).toBeUndefined()
    expect(classifyCommit('fix: x', [src])).toBeUndefined()
    expect(classifyCommit('fix: x', ['packages/a/b/src/types.d.ts', spec])).toBeUndefined()
    expect(classifyCommit('fix: x', [spec, 'packages/a/b/src/1.ts', 'packages/a/b/src/2.ts', 'packages/a/b/src/3.ts', 'packages/a/b/src/4.ts'])).toBeUndefined()
    expect(classifyCommit('fix: x', [src, spec], { maxSourceFiles: 3, maxChangedFiles: 1 })).toBeUndefined()
  })
})

describe('parseGitLog', () => {
  it('splits NUL-separated commits into hash, parents, subject, and files', () => {
    const log = '\0aaa\tppp\tfix: one\n\nsrc/a.ts\ntests/a.spec.ts\n\0bbb\tp1 p2\tmerge\n\n'
    expect(parseGitLog(log)).toEqual([
      { hash: 'aaa', parents: ['ppp'], subject: 'fix: one', files: ['src/a.ts', 'tests/a.spec.ts'] },
      { hash: 'bbb', parents: ['p1', 'p2'], subject: 'merge', files: [] },
    ])
  })
})

describe('taskPrompt', () => {
  it('shows the failing tests and forbids editing them without naming the source', () => {
    const prompt = taskPrompt({
      id: 'abc',
      fixCommit: 'f',
      parentCommit: 'p',
      subject: 'fix: secret subject',
      sourceFiles: ['packages/a/b/src/hidden.ts'],
      testFiles: ['packages/a/b/tests/b.spec.ts'],
    }, '  FAIL b.spec.ts > keeps order  ')
    expect(prompt).toContain('- packages/a/b/tests/b.spec.ts')
    expect(prompt).toContain('FAIL b.spec.ts > keeps order')
    expect(prompt).toContain('Do not modify the test files.')
    expect(prompt).not.toContain('hidden.ts')
    expect(prompt).not.toContain('secret subject')
  })
})

describe('mining and preparing from a real repository', () => {
  async function commit(repo: string, files: Record<string, string>, message: string): Promise<void> {
    for (const [path, content] of Object.entries(files)) {
      await mkdir(join(repo, path, '..'), { recursive: true })
      await writeFile(join(repo, path), content)
    }
    await git('git', ['add', '-A'], { cwd: repo })
    await git('git', ['-c', 'user.name=eval', '-c', 'user.email=eval@example.com', 'commit', '-q', '-m', message], { cwd: repo })
  }

  it('mines the fix and prepares a workspace with the source reverted, the tests kept, and no history', async () => {
    root = await mkdtemp(join(tmpdir(), 'dsh-eval-tasks-'))
    const repo = join(root, 'repo')
    await mkdir(repo)
    await git('git', ['init', '-q'], { cwd: repo })
    const src = 'packages/core/math/src/add.ts'
    const spec = 'packages/core/math/tests/add.spec.ts'
    await commit(repo, { [src]: 'export const add = (a, b) => a - b\
... [3,525 more characters in session.jsonl]

#### ASSISTANT

_[empty]_

_stop `null` · 1.28s · in 0 · out 0 · cache r0/w0_

---

## req-0002 — claude-opus-5-5

_buffered · 1 messages_

_[no new input since the previous request]_

#### ASSISTANT

_[empty]_

_stop `null` · 1.06s · in 0 · out 0 · cache r0/w0_

