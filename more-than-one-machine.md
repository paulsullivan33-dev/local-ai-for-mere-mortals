# More Than One Machine

One machine can host the models while others use them. The common
shape: a desktop with a good GPU does the heavy thinking, and a
laptop, a Raspberry Pi, or a phone on the same home network sends
it questions through the API. The small machine needs no GPU at
all — it just sends text and gets text back.

## OLLAMA_HOST, in plain language

By default, Ollama's API listens on **localhost** — only programs
on that same machine can reach it. That's the safe default from
[The Ollama API](ollama-api.md).

To let other machines on your home network reach it, you set an
environment variable **before Ollama starts**:

| System | How to set it |
|--------|---------------|
| Linux / Mac (terminal) | `export OLLAMA_HOST=0.0.0.0:11434` then start Ollama from that terminal |
| Windows | `setx OLLAMA_HOST "0.0.0.0"` in a command prompt, then quit and restart the Ollama app |

`0.0.0.0` means "listen on all network interfaces, not just
localhost." After that, other machines reach the API at:

```text
http://<host-machine's-address>:11434
```

The host machine's address is its **LAN address** — something like
`192.168.1.50`, found in your network settings — *not* `localhost`,
which on the other machine would mean itself.

**Check:** from the second machine, open
`http://<host-address>:11434/api/tags` in a browser or with curl.
You should see the host's model list. If it refuses, see
[Troubleshooting](troubleshooting.md).

## Which machine does what

| Machine | Job | Needs |
|---------|-----|-------|
| The host (e.g., a desktop with a good GPU) | Runs Ollama, holds the models, does the math | Memory for the model (the [size formula](how-models-fit-in-memory.md) still rules) |
| The clients (laptop, Pi, anything) | Send prompts, display answers | Just a network connection |

A Raspberry Pi makes a fine client: it can't comfortably *run* an
8B model, but it can *ask* a desktop to run one all day.

## Safety: home network only

Read this twice:

- `OLLAMA_HOST=0.0.0.0` exposes the API to **everyone on your
  network** — anyone connected can use your models and read your
  prompts. On a home network you control, that's usually fine.
- **Do not forward port 11434 on your router.** That would expose
  the API to the entire internet — strangers running prompts on
  your hardware, on your electricity. There is no login on the
  Ollama API; the network boundary *is* the security.
- When in doubt, leave the default (localhost-only). You lose
  nothing except remote access.

Local models can still produce wrong or harmful content, and now
that content can come from any machine on your network. The privacy
win of local AI — your words stay home — only holds if "home"
doesn't accidentally include the whole internet.

**Next:** [Troubleshooting](troubleshooting.md)
