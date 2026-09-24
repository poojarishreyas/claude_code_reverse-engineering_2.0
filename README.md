# Claude Code trajectories

Captured by **ccproxy** - a local proxy sitting between the Claude Code CLI and the
Anthropic API. Every request and response is recorded, then committed here.

## Layout

```
sessions/<YYYY-MM-DD>/<session-id>/
    session.jsonl    append-only event log - the source of truth
    manifest.json    summary: model, request count, token usage, timings
    transcript.md    human-readable rendering of the same log
objects/<xx>/<id>.json
    content-addressed payloads (messages, system prompts, tool catalogues),
    each stored exactly once and referenced by id from the logs
INDEX.md             table of every captured session, newest first
```

## Event vocabulary

| type | meaning |
| --- | --- |
| `session/start` | first request of a conversation observed |
| `request/context` | effective system prompt / tool catalogue changed |
| `request/start` | one model request left the CLI |
| `response/open` | upstream responded; status and headers recorded |
| `response/chunks` | streamed SSE deltas, packed into runs |
| `response/message` | assembled reply, stop reason, usage, timings |
| `response/error` | upstream returned a non-2xx status, or the hop failed |

## Secrets

Credentials are fingerprinted, never stored: `x-api-key` and `authorization` become a
stable `redacted` digest, so sessions stay distinguishable by key without exposing it.
Known credential shapes (`sk-ant-`, `ghp_`, `AKIA`, PEM blocks) are scrubbed from bodies.
