# import { describe, expect, it, vi } from 'vitest' import { AttachmentId, ImageVariantId } from '@deepseek-ai/dsh-atta...

| | |
| --- | --- |
| session | `s-a537d6379f878f80` |
| model | `claude-opus-5-5` |
| started | 2026-10-08T08:39:53.616Z |
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

import { describe, expect, it, vi } from 'vitest'
import { AttachmentId, ImageVariantId } from '@deepseek-ai/dsh-attachment'
import type { AttachmentStore, ImageAttachmentRef, ImageRequestPolicy, RequestImageAttachment } from '@deepseek-ai/dsh-attachment'
import { createUserMessage, ToolCallId, CONTEXT_WINDOW_EXCEEDED_CODE, EMPTY_RESPONSE_CODE, createMessage } from '@deepseek-ai/dsh-llm'
import type { ContentBlock, StreamChunk } from '@deepseek-ai/dsh-llm'
import type { AssistantMessage, AssistantMessageEvent, Usage } from '@earendil-works/pi-ai'
import { toPiContext } from '../src/context.ts'
import { toPiReplayState } from '../src/replay.ts'
import { mapStopReason, mapUsage, toStreamChunks } from '../src/stream.ts'

function usage(input = 0, output = 0, cacheRead = 0, cacheWrite = 0): Usage {
  return {
    input,
    output,
    cacheRead,
    cacheWrite,
    totalTokens: input + output + cacheRead + cacheWrite,
    cost: { input: 0, output: 0, cacheRead: 0, cacheWrite: 0, total: 0 },
  }
}

function assistant(overrides: Partial<AssistantMessage> = {}): AssistantMessage {
  return {
    role: 'assistant',
    content: [],
    api: 'openai-completions',
    provider: 'deepseek',
    model: 'deepseek-v4-flash',
    usage: usage(),
    stopReason: 'stop',
    timestamp: 0,
    ...overrides,
  }
}

async function* feed(...events: AssistantMessageEvent[]): AsyncGenerator<AssistantMessageEvent> {
  for (const event of events) yield event
}

async function collect(stream: AsyncIterable<StreamChunk>): Promise<StreamChunk[]> {
  const out: StreamChunk[] = []
  for await (const chunk of stream) out.push(chunk)
  return out
}

function requestVersion(ref: ImageAttachmentRef): RequestImageAttachment {
  return {
    variantId: ImageVariantId(`sha256:${'e'.repeat(64)}`),
    attachment: ref,
    data: Uint8Array.of(1, 2, 3),
    mediaType: ref.mediaType,
    bytes: 3,
    width: ref.width,
    height: ref.height,
    depth: 'uchar',
    space: 'srgb',
    hasAlpha: true,
  }
}

function attachmentStore(readImageRequest: (
  ref: ImageAttachmentRef,
  policy: ImageRequestPolicy,
  signal?: AbortSignal,
) => Promise<RequestImageAttachment>): AttachmentStore {
  return { readImageRequest, imageHostPath: () => undefined } as unknown as AttachmentStore
}

function imageContext(attachments: AttachmentStore) {
  return { attachments, resolveImageAccess: () => undefined }
}

describe('toPiContext', () => {
  it('maps system prompt, user text, and tools', () => {
    const context = toPiContext({
      provider: 'deepseek',
      model: 'deepseek-v4-flash',
      system: 'be helpful',
      messages: [createUserMessage({
        content: [{ type: 'text', text: 'hi' }],
        source: { kind: 'plugin', plugin: 'test' },
      })],
      tools: [{ name: 'f', description: 'F', parameters: { type: 'object', properties: {} } }],
    })
    expect(context.systemPrompt).toBe('be helpful')
    expect(context.messages).toEqual([{ role: 'user', content: 'hi', timestamp: 0 }])
    expect(context.tools).toEqual([
      { name: 'f', description: 'F', parameters: { type: 'object', properties: {} } },
    ])
  })

  it('omits empty tools and absent system prompt', () => {
    const context = toPiContext({ provider: 'deepseek', model: 'm', messages: [], tools: [] })
    expect(context.systemPrompt).toBeUndefined()
    expect(context.tools).toBeUndefined()
  })

  it('resolves durable image references into native pi-ai image content', async () => {
    const attachment = {
      attachmentId: AttachmentId(`sha256:${'a'.repeat(64)}`),
      mediaType: 'image/png' as const,
      bytes: 3,
      width: 1,
      height: 1,
    }
    const readImageRequest = vi.fn((value: ImageAttachmentRef, _policy: ImageRequestPolicy) => (
      Promise.resolve(requestVersion(value))
    ))
    const context = await toPiContext({
      provider: 'openai',
      model: 'gpt-4.1',
      messages: [createUserMessage({
        content: [{ type: 'text', text: 'describe' }, { type: 'im
... [33,381 more characters in session.jsonl]

#### ASSISTANT

_[empty]_

_stop `null` · 685ms · in 0 · out 0 · cache r0/w0_

