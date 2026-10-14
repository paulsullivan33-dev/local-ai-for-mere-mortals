# How Models Fit in Memory

A model is mostly one giant pile of numbers — its **parameters**.
("8b" means 8 billion of them.) Every number has to live in memory
while the model runs, so the model's memory footprint is roughly:

> **GB ≈ (billions of parameters) × (bytes per parameter)**

That's the size formula. You'll use it for everything in this
guide. The second half — bytes per parameter — depends on
**quantization**: how precisely each number is stored.

## Quantization, simply

A parameter can be stored as a precise number (lots of bytes) or a
rounded-off number (few bytes). Rounding makes the file smaller;
the model gets slightly less precise. Quantization is that
rounding, done carefully so the quality loss stays small.

| Format | Bytes per parameter | What it means |
|--------|--------------------|---------------|
| FP16 | 2.0 | Full precision — the reference, biggest file |
| Q8_0 | ≈ 1.0 | Light rounding — close to full quality, half the size |
| Q4_K_M | ≈ 0.6 | Heavier rounding — much smaller, small quality cost |

Q4_K_M is the everyday default: it's what you'll usually download,
and it's the basis for every size figure in this guide unless a
chapter says otherwise.

## The formula in action

An 8-billion-parameter model at Q4_K_M:

> 8 × 0.6 ≈ **4.8 GB**

The same model at Q8_0: 8 × 1.0 ≈ **8 GB**. At FP16: 8 × 2.0 =
**16 GB**. Same brain, three file sizes — pick your trade.

## The canonical table (Q4_K_M)

| Parameters | Memory (formula) | Stated as |
|------------|-----------------|-----------|
| 1B | 1 × 0.6 = 0.6 | **≈ 0.8 GB** |
| 3B | 3 × 0.6 = 1.8 | **≈ 2 GB** |
| 8B | 8 × 0.6 = 4.8 | **≈ 4.8 GB** |
| 14B | 14 × 0.6 = 8.4 | **≈ 8.4 GB** |
| 32B | 32 × 0.6 = 19.2 | **≈ 19 GB** |
| 70B | 70 × 0.6 = 42 | **≈ 42 GB** |

Every size claim in this guide matches this table or shows its
math — no exceptions. (The 1B row says 0.8, not 0.6, because tiny
models carry a bit of fixed overhead — vocabulary, metadata — that
the formula doesn't count. The overhead matters less as models get
bigger.)

A sense of scale: a 405-billion-parameter model at Q4_K_M would be
405 × 0.6 ≈ **243 GB**. That's not a home-machine model — which is
exactly why the formula matters. It tells you *before* downloading.

## The conversation also costs memory

The model file isn't the whole story. While you chat, the model
keeps a kind of scratch paper — the **KV cache** — remembering what
was said so it doesn't recompute it every time. Longer
conversations need more scratch paper.

**Rough formula (order of magnitude only — depends on the model
and setup):** the cache grows with the length of the conversation
times the width of the model. As a very rough feel: for an 8B-class
model, a few thousand tokens of conversation costs on the order of
half a GB extra; a very long chat (tens of thousands of tokens) can
cost several GB extra.

Don't budget to the decimal from that — treat it as "leave
headroom." Rule of thumb: the model file, the conversation cache,
and your operating system all share the same pool, so a 4.8 GB
model wants comfortably more than 4.8 GB free.

**Check:** pick any model size you like and run the formula. 14B at
Q4_K_M → 14 × 0.6 ≈ 8.4 GB. Matches the table? Then you've got it.

**Next:** [Hardware](hardware.md)
