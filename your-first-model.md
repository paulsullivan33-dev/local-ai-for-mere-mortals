# Your First Model

**Ollama** is the simplest way to run models locally: one program
that downloads models, runs them, and serves them to you and your
programs. This chapter gets you chatting in minutes.

## Install it

**Linux** — one line in a terminal:

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

**Mac or Windows** — download the installer from
[ollama.com](https://ollama.com) and run it. (No command line
needed for the install itself.)

**Check:** confirm it's there:

```bash
ollama --version
```

You should see a version number printed back. If the command isn't
found, the install didn't finish — re-run the step above.

## Download a small model

Start small. **tinyllama** is a 1-billion-parameter model — about
0.8 GB by the [size formula](how-models-fit-in-memory.md) — so it
fits almost anywhere and downloads quickly:

```bash
ollama pull tinyllama
```

**Check:** the download completes, and then:

```bash
ollama list
```

shows `tinyllama` in your local model list.

## Chat

```bash
ollama run tinyllama
```

If the model isn't downloaded yet, `run` fetches it first — `pull`
and `run` in one step. You'll get a `>>>` prompt. Type something:

```text
>>> Write a haiku about a rainy Tuesday.
```

The model answers, word by word, right in your terminal. Ask a few
things. Notice it's small — answers are simple, sometimes clumsy.
That's a 1B model being honest about its size.

Two commands to know inside the chat: `/help` lists the chat
commands, and `/bye` exits back to your terminal.

## The other commands you'll actually use

| Command | What it does |
|---------|--------------|
| `ollama pull <model>` | Download a model |
| `ollama run <model>` | Chat with a model (downloads it first if needed) |
| `ollama list` | Show your downloaded models |
| `ollama ps` | Show models currently loaded and running |
| `ollama rm <model>` | Delete a model to free disk space |
| `ollama show <model>` | Show details about a model |
| `ollama --version` | Show the Ollama version |

**Check:** run `ollama ps` while a chat is open in another
terminal — you'll see your model listed as loaded. Close the chat
with `/bye` and check again later: Ollama unloads idle models on
its own to free memory.

That's the whole loop: pull, run, chat. The next chapter is about
getting better answers out of the conversation.

**Next:** [Talking to Models](talking-to-models.md)
