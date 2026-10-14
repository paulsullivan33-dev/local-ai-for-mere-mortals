# Choosing Models

The Ollama library holds dozens of models. Picking one comes down
to three questions: how big is it (the [size
formula](how-models-fit-in-memory.md)), what was it tuned for, and
how heavily its numbers are rounded. This chapter teaches you to
read the label.

## Reading a model card

Every model in the Ollama library has a page — its **model card** —
listing the available sizes, quantization options, and what the
model was tuned for. Before downloading, check three things:

1. **Parameter size** (`8b`, `3b`, `1b`…) — run the size formula.
   If the answer is bigger than your free memory, stop here.
2. **Tuning** — chat, code, or something specialized. For general
   chatting, grab an instruct model (see [Talking to
   Models](talking-to-models.md)).
3. **Quantization options** — usually several; the default is
   normally the sensible pick.

Well-known general-chat models in the library include `llama3.1`,
`qwen3`, `gemma3` (in several sizes each), and the tiny `tinyllama`
(1B). Start with one of these before exploring further.

## Decoding the size label

`qwen3:8b` = the qwen3 family, 8 billion parameters → 8 × 0.6 ≈
**4.8 GB** at Q4_K_M. `gemma3:4b` = 4 billion → 4 × 0.6 ≈ **2.4
GB**. The number before the "b" goes straight into the formula.
Some models also carry a quantization suffix after the size —
that's the next section.

## Quantization suffixes, decoded

You'll see tags like `llama3.1:8b-instruct-q4_K_M`. Reading right
to left after the size:

| Suffix | Plain meaning |
|--------|---------------|
| `Q4_K_M` | ~4 bits per weight ("K" = newer K-quant scheme, "M" = medium among S/M/L variants) — the everyday default |
| `Q4_K_S` | Same family, "small" — slightly smaller file, slightly more rounding |
| `Q4_0` | Older 4-bit scheme — fine, just not the newest |
| `Q5_K_M`, `Q6_K` | More bits, bigger file, closer to full precision |
| `Q8_0` | ~1 byte per weight — near-full quality at about double the Q4 size |
| `FP16` | Full 16-bit precision — the reference; 2 bytes per parameter, biggest file |

The trade is always the same: **more bits = bigger file = slightly
better answers**. Q4_K_M is the sweet spot for most home use; Q8_0
is for when you have memory to spare and want the extra fidelity;
FP16 is for benchmarking, not for daily driving.

Worked comparison for an 8B model: Q4_K_M ≈ **4.8 GB**, Q8_0 = 8 ×
1.0 ≈ **8 GB**, FP16 = 8 × 2.0 = **16 GB**. Same model, three
prices.

## Matching model to use case

| Situation | Sensible pick |
|-----------|---------------|
| Tiny machine / learning the ropes | `tinyllama` — 1B, ≈ 0.8 GB |
| General chat on a decent PC or M-series Mac | An 8B-class instruct model (`llama3.1`, `qwen3`, or `gemma3`) — ≈ 4.8 GB |
| Weaker machine that still wants decent chat | A 3B-class model — ≈ 2 GB |
| Curiosity about the biggest home-runnable | 32B (≈ 19 GB) or 70B (≈ 42 GB) — only if the memory math works |

Two principles: **fit first** — the best model is one that actually
loads with headroom to spare — and **don't chase the biggest**; an
8B model that runs smoothly beats a 32B model that doesn't fit.

## Model updates

Models don't update themselves. When a new version appears in the
library, you `ollama pull` it again — same command as the first
download. Old versions stay until you `ollama rm` them, so check
`ollama list` now and then and delete what you no longer use. Disk
space is the quiet cost of curiosity: five 8B models is five times
4.8 GB.

**Check:** before your next download, write down the size label,
run the formula, and compare against your free memory. If the habit
sticks, you'll never download a model you can't run.

**Next:** [Tools and Function Calling](tools-and-function-calling.md)
