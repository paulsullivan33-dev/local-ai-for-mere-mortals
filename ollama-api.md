# The Ollama API

Ollama isn't just a chat program — while it runs, it also serves a
**local API**: a web address on your own machine that your programs
can talk to. The base address is:

```text
http://localhost:11434
```

"localhost" means *this machine* — nothing leaves your computer.
Three endpoints cover nearly everything.

## List your models: `/api/tags`

```bash
curl http://localhost:11434/api/tags
```

**Check (example shape — your model names will differ):**

```json
{"models": [{"name": "tinyllama:latest", "...": "..."}]}
```

You get back a list of what's downloaded. If this fails with
"connection refused," Ollama isn't running — start any `ollama run`
and try again. (More on that in
[Troubleshooting](troubleshooting.md).)

## Generate text: `/api/generate`

```bash
curl http://localhost:11434/api/generate \
  -d '{"model": "tinyllama", "prompt": "Why is the sky blue?", "stream": false}'
```

The pieces, same as any API call:

| Piece | Meaning |
|-------|---------|
| The URL | `/api/generate` — "make text" |
| `"model"` | Which downloaded model to use |
| `"prompt"` | What to say to it |
| `"stream": false` | Wait for the whole answer (see below) |

**Check (example shape — the wording depends on the model):**

```json
{"model": "tinyllama", "response": "The sky is blue because..."}
```

Your program reads the `response` field. That's the whole
integration: send JSON, get JSON.

## Chat with history: `/api/chat`

`/api/generate` is one question, one answer. `/api/chat` keeps a
conversation — you send the message history, with roles:

```bash
curl http://localhost:11434/api/chat \
  -d '{
    "model": "tinyllama",
    "stream": false,
    "messages": [
      {"role": "system", "content": "Answer in short sentences."},
      {"role": "user", "content": "What is photosynthesis?"},
      {"role": "assistant", "content": "Plants make food from sunlight."},
      {"role": "user", "content": "What do they need for it?"}
    ]
  }'
```

Roles: `system` sets the behavior (the [system
prompt](talking-to-models.md)), `user` is you, `assistant` is the
model's earlier replies. **You** keep the history — send the whole
list each time, appending the latest exchange. The model itself
remembers nothing between calls.

**Check (example shape):**

```json
{"model": "tinyllama", "message": {"role": "assistant", "content": "..."}}
```

## Streaming, the concept

By default (`"stream"` not set, or `true`), the API sends the
answer back in pieces — one JSON object per chunk — as the words
are generated. That's **streaming**: your program can display words
as they arrive instead of waiting for the whole answer, which feels
much faster even though the total time is the same. `"stream":
false` waits and returns one complete object — simpler for scripts.

## Safety note

This API listens on localhost by default: only programs on *your*
machine can reach it. That's the safe default — keep it that way
unless you know why you're changing it. Opening it to other
machines is covered in [More Than One
Machine](more-than-one-machine.md), with the warnings attached.

**Next:** [Open WebUI](open-webui.md)
