# Local AI at Home for Mere Mortals

**Cloud AI** means your words travel to someone else's computer,
which thinks and answers back. **Local AI** means the thinking
happens on *your* computer — the model file sits on your disk, and
your questions never leave the house. This guide teaches you to run
AI models on your own machines: why you'd bother, what fits in
memory, and how to chat with a model, use its API, and keep it
running.

No CS degree required. This is the hands-on companion to [AI for
Mere Mortals](https://paulsullivan33-dev.github.io/AI-for-mere-mortals/),
which explains what language models *are*. That guide covers the
ideas; this one covers the operating.

## What this guide covers

- **What local AI is** — cloud vs. local, and the honest trade-offs
- **How models fit in memory** — parameters, quantization, and the
  size formula you'll use for everything
- **Hardware** — CPU vs. GPU vs. Apple Silicon vs. Raspberry Pi, in
  generic terms, and what each tier can comfortably run
- **Your first model** — installing Ollama and chatting in minutes
- **Talking to models** — system prompts, temperature, instruct vs.
  base models, what "8b" means
- **The Ollama API** — `/api/generate`, `/api/chat`, `/api/tags`
  with curl
- **Open WebUI** — a ChatGPT-like interface for your local models
- **Choosing models** — reading a model card, decoding quantization
  suffixes, matching model to machine
- **Tools and function calling** — letting a model call *your* code
- **More than one machine** — hosting models on one box, using them
  from another
- **Troubleshooting** — symptom → fix for the common failures
- **Glossary** — every jargon term, collected

## What it doesn't cover

How language models work inside (transformers, training — that's
the [AI for Mere Mortals](https://paulsullivan33-dev.github.io/AI-for-mere-mortals/)
guide), training or fine-tuning your own model, production serving,
or cloud model APIs. This guide is about *running* models at home.

## How to use this guide

Every `ollama` command in this guide was checked against the real
Ollama CLI (version 0.40.3), and the API examples in [The Ollama
API](ollama-api.md) were run against a live local server with a
real model — **Check:** blocks show real output. Two honest notes:
downloading from the public model registry wasn't completed on the
writing machine (a network quirk), so `ollama pull` is documented
from the verified CLI rather than a measured download; and the
Open WebUI install is described from the project's docs, not run
here. Run the steps yourself — that's the point. Size figures
throughout come from one formula (see [How Models Fit in
Memory](how-models-fit-in-memory.md)), stated every time it's used.

Two safety notes, up front: a local model can still produce wrong or
harmful content — "local" doesn't mean "safe." And the local API
should stay on your home network; exposing it to the internet needs
care (see [More Than One Machine](more-than-one-machine.md)).

## Chapters

1. [What Is Local AI?](what-is-local-ai.md)
2. [How Models Fit in Memory](how-models-fit-in-memory.md)
3. [Hardware](hardware.md)
4. [Your First Model](your-first-model.md)
5. [Talking to Models](talking-to-models.md)
6. [The Ollama API](ollama-api.md)
7. [Open WebUI](open-webui.md)
8. [Choosing Models](choosing-models.md)
9. [Tools and Function Calling](tools-and-function-calling.md)
10. [More Than One Machine](more-than-one-machine.md)
11. [Troubleshooting](troubleshooting.md)
12. [Glossary](glossary.md)

*Written to the [nine-point writing standard](criteria.md) shared by
every guide in this series.*
