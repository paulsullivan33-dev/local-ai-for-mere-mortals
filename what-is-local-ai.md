# What Is Local AI?

When you use a cloud AI service, your words travel to someone
else's computer. That computer runs the model, thinks, and sends an
answer back. **Local AI** flips that around: the model file sits on
*your* disk, the thinking happens on *your* processor, and your
words never leave the house.

Think of it like the difference between a calculator app on your
phone and a website that does math for you. Both give answers; one
needs the internet and someone else's server, the other just works.

This guide is the hands-on companion to **AI for Mere Mortals**,
which explains what language models *are*. That guide covers the
ideas (tokens, training, why models sometimes make things up). This
one covers the operating: getting a model onto your machine and
using it. It won't re-teach the internals.

## The trade, honestly

| | Cloud AI | Local AI |
|---|---|---|
| Your words go to | Someone else's server | Nowhere — they stay home |
| Cost | Per-message or subscription | Free after setup (plus electricity) |
| Internet needed? | Yes, always | No, once the model is downloaded |
| Model strength | The biggest, newest models | Weaker than the frontier cloud models |
| Updates | Automatic | You download new versions yourself |
| Tech support | Their problem | Your problem |

The rows at the bottom matter. The largest cloud models are far
bigger than anything that fits on a home machine — a local model
will not match them answer-for-answer. And nobody maintains your
setup for you: when a better version of a model comes out, you
fetch it. That's the price of the privacy and control.

## Why run local

- **Privacy.** Medical notes, journal entries, work documents —
  some things you simply don't want uploaded. Locally, they aren't.
- **Cost.** After the hardware you already own, there's no
  per-message meter running. Experiment freely.
- **Offline.** On a plane, at a cabin, during an outage — a
  downloaded model doesn't care about your connection.
- **Tinkering.** You choose the model, the version, the settings.
  Nothing changes under you overnight unless you change it.

## What local can't do

- **Match the biggest cloud models.** An 8B model (≈ 4.8 GB) is not
  going to out-reason one that needs a data center.
  Local models are genuinely useful; they are genuinely smaller.
- **Update itself.** New model versions arrive when you download
  them, not before.
- **Guarantee good answers.** A local model can still be wrong,
  confident, or unhelpful — "runs on my machine" is not a quality
  stamp. Verify anything important, same as with cloud AI.

If that trade sounds fair — your hardware, your data, your
maintenance — the next question is practical: what actually fits in
memory?

**Next:** [How Models Fit in Memory](how-models-fit-in-memory.md)
