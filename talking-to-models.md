# Talking to Models

Chatting is easy; getting *good* answers takes a little technique.
This chapter covers the four ideas that matter most: what the size
label means, the system prompt, temperature, and instruct vs. base
models.

## What "8b" means

A name like `llama3.1:8b` has two parts: the model family
(`llama3.1`) and the size (`8b` = 8 billion parameters). By the
[size formula](how-models-fit-in-memory.md), that's about 4.8 GB at
Q4_K_M.

Bigger generally means more capable — an 8B model writes better
than a 1B model — but also more memory and slower answers on the
same hardware. Size is the main dial you turn when a model feels
too weak or too slow.

## The system prompt

Every conversation has a hidden instruction the model sees before
your words — the **system prompt**. It sets the role: "You are a
helpful assistant" is the default; "Answer in short bullet points"
or "You are a patient tutor" changes the flavor of everything
after.

You can set your own. In Open WebUI (see [Open
WebUI](open-webui.md)) there's a field for it; through the API you
send it as a `system` message (see [The Ollama
API](ollama-api.md)). Before/after:

| Without a system prompt | With "Explain like I'm new, and use short sentences" |
|---|---|
| A correct but dense paragraph | The same idea, in plain short sentences |

Small models benefit the most: a clear system prompt keeps a 1B
model on track where it would otherwise wander.

## Temperature, in plain language

**Temperature** controls how predictable the model's word choices
are:

- **Low (near 0):** the model picks the most likely next word every
  time. Focused, consistent, a bit dry. Good for facts, summaries,
  code.
- **High (near 1 and up):** the model rolls the dice more. Varied,
  creative, and more likely to go off the rails. Good for
  brainstorming, bad for instructions.

The default is fine for most chatting. If you want to change it,
the API takes an option like this (see the [API
chapter](ollama-api.md) for the full call):

```json
{"options": {"temperature": 0.2}}
```

Lower for "just the facts," higher for "surprise me." There is no
universally right value — it's a preference dial, not a quality
dial.

## Instruct vs. base models

Models come in two flavors, and you almost always want the first:

- **Instruct models** are trained to follow instructions and hold a
  conversation. `llama3.1`, `qwen3`, `gemma3` in the Ollama library
  are instruct models — the ones you chat with.
- **Base models** are raw autocomplete: trained only to predict the
  next word of internet text. Give one a question and it may just
  continue the question. Interesting for researchers; useless for
  chatting.

If a model seems to ignore your questions and ramble instead, check
whether you grabbed a base variant by mistake.

## Practical habits

- **Be specific.** "Summarize this article in three bullets" beats
  "tell me about this."
- **One thing at a time.** Long, multi-part requests confuse small
  models; split them up.
- **Match the prompt to the size.** A 1B model does best with
  short, simple instructions. Save the subtle stuff for bigger
  models.
- **Verify.** Any model, any size, can state something false with
  total confidence. Local doesn't mean reliable — check anything
  important.

**Check:** set a system prompt ("Answer everything as a limerick")
and ask two questions. Then clear it and ask again. The difference
you feel is the system prompt doing its job.

**Next:** [The Ollama API](ollama-api.md)
